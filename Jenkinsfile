pipeline {
    
    agent any 
    
    environment { 
        registry = "kingashok9/cicd-e2e:v1" 
        registryCredential = 'kingashok9_hub' 
        dockerImage = '' 
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
                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 
                }
            }
        }

        stage('Push the artifacts'){
           steps { 
               script { 
                   docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push() 
                    }
                } 
            }
        }
        
                
        
    }
}    
    
