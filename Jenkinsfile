pipeline {
    agent any

    tools {
        maven 'Maven_3.9.11'   // Name from Jenkins "Global Tool Configuration"
        jdk 'Java_21'          // Name from Jenkins "Global Tool Configuration"
    }

    triggers {
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Suhana786-s/Practice.git'
            }
        }

        stage('Build JAR') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Unit Tests') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Version Document') {
            steps {
                bat 'echo Build Version: > version.txt'
                bat 'mvn help:evaluate -Dexpression=project.version -q -DforceStdout >> version.txt'
                bat 'echo Build Time: %DATE% %TIME% >> version.txt'
                archiveArtifacts artifacts: 'version.txt'
            }
        }

  



    }

    post {
        success {
            echo "Build and Deploy completed successfully!"
        }
        failure {
            echo "Build failed!"
        }
    }
}