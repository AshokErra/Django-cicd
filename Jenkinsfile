pipeline {
    
    agent any 
    
    environment {
         DOCKER_HUB_CREDENTIALS = credentials('kingashok9')
        // Define the Docker image name and tag
        DOCKER_IMAGE_NAME = "kingashok9/cicd-e2e"
        DOCKER_IMAGE_TAG = "latest"
    }
    
    stages {
        
        stage('Checkout'){
           steps {
                 git credentialsId: '368ec86f-298d-4187-a660-88f3e58c59a2', 
                url: 'https://github.com/AshokErra/Django-cicd',
                branch: 'main'
           }
        }

        stage('Build Docker'){
            steps{
                script{
                    sh '''
                    echo 'Buid Docker Image'
                    docker build -t kingashok9/cicd-e2e:${DOCKER_IMAGE_TAG} .
                    '''
                }
            }
        }

        stage('Push the artifacts'){
           steps{
                script{
                    
                    docker.withRegistry('https://registry.hub.docker.com', DOCKER_HUB_CREDENTIALS) {
                        docker.image("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}").push()
                    }
                    
                }
            }
        }
    }
}
