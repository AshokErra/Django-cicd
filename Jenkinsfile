pipeline {
    agent any

    environment {
        // Define your Docker Hub credentials
        DOCKER_HUB_CREDENTIALS = credentials('kingashok9_hub')
        // Define the Docker image name and tag
        DOCKER_IMAGE_NAME = "kingashok9/Django-cicd"
        DOCKER_IMAGE_TAG = "latest"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from your version control system
                git credentialsId: '368ec86f-298d-4187-a660-88f3e58c59a2', 
                url: 'https://github.com/AshokErra/Django-cicd',
                branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the Docker image using the Dockerfile in the project root
                script {
                    docker.build("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                // Push the Docker image to the Docker Hub registry
                script {
                    docker.withRegistry('https://registry.hub.docker.com', DOCKER_HUB_CREDENTIALS) {
                        docker.image("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}").push()
                    }
                }
            }
        }
    }
}
    
