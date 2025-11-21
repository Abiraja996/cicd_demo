pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker_hub_token')
        IMAGE_NAME = "abishek996/cicd-demo"
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Abiraja996/cicd_demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    bat "docker build -t ${IMAGE_NAME}:latest ."
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    bat """
                    echo %DOCKERHUB_CREDENTIALS_PSW% | docker login -u %DOCKERHUB_CREDENTIALS_USR% --password-stdin
                    """
                }
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                script {
                    bat "docker push ${IMAGE_NAME}:latest"
                }
            }
        }
    }
}
