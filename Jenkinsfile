pipeline {
    agent any

    environment {
        IMAGE_NAME = "pawan82353/python-app"
        IMAGE_TAG = "latest"
        DOCKER_CREDENTIALS = "dockerhub-credentials"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS) {
                        docker.image("${IMAGE_NAME}:${IMAGE_TAG}").push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Docker image built and pushed successfully!'
        }

        failure {
            echo 'Pipeline failed.'
        }
    }
}
