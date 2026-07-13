pipeline {
    agent any

    environment {
        DOCKERHUB_USERNAME = "madhu58"
        IMAGE_NAME = "market-app"
        IMAGE_TAG = "latest"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    bat 'echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin'
                }
            }
        }

        stage('Build Image') {
            steps {
                bat 'docker build -t %DOCKERHUB_USERNAME%/%IMAGE_NAME%:%IMAGE_TAG% .'
            }
        }

        stage('Push Image') {
            steps {
                bat 'docker push %DOCKERHUB_USERNAME%/%IMAGE_NAME%:%IMAGE_TAG%'
            }
        }
    }
}