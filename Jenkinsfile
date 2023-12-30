pipeline {
    
    agent any 
     
    stages {
        
        stage('Checkout'){
           steps {
                 git credentialsId: '368ec86f-298d-4187-a660-88f3e58c59a2', 
                url: 'https://github.com/AshokErra/Django-cicd',
                branch: 'main'
           }
        }
     
    stage("Docker Build & Push"){
            steps{
                script{
                   withDockerRegistry(credentialsId: 'kingashok9_hub', toolName: 'docker'){   
                       sh "docker build -t cicd-e2e ."
                       sh "docker tag cicd-e2e kingashok9/cicd-e2e:latest "
                       sh "docker push kingashok9/cicd-e2e:latest "
                    }
                }
            }
        }
        stage('Checkout'){
           steps {
                 git credentialsId: '368ec86f-298d-4187-a660-88f3e58c59a2', 
                url: 'https://github.com/AshokErra/Django-cicd/deploy',
                branch: 'main'
           }
        }
        stage('Deploy to kubernets'){
            steps{
                script{
                    withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'K8S', namespace: '', restrictKubeConfigAccess: false, serverUrl: '') {
                       sh 'kubectl apply -f deploy.yaml'
                  }
                }
            }
        }
    }
}
