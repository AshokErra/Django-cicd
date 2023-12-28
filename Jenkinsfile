pipeline {
    
    agent any 
    
    environment { 
        IMAGE_TAG = "${BUILD_NUMBER}"
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
            steps { 
                script { 
                    sh '''
                    echo 'Buid Docker Image'
                    docker build -t kingashok9/cicd-e2e:${BUILD_NUMBER} .
                    '''
                }
            }
        }

        stage('Push the artifacts'){
           steps { 
               script { 
                   sh '''
                    echo 'Push to Repo'
                    docker push kingashok9/cicd-e2e:${BUILD_NUMBER}
                    '''
                } 
            }
        }    
    }
}    
    
