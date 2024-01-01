pipeline {
    
    agent any 
    environment {
        KUBECONFIG = '/home/ashokvm/.kube/config'
    }
     
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
        stage('Deploy to container'){
            steps{
                sh 'docker run -d --name cicd-e2e -p 3000:3000 kingashok9/cicd-e2e:latest'
            }
        }
        stage('Deploy to kubernets'){
            steps{
                script{
                    def kubeconfig = readFile '/home/ashokvm/.kube/config'
                    withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'k8s', namespace: '', restrictKubeConfigAccess: false, serverUrl: '') {
                       sh 'kubectl apply -f deploy.yaml'
                  }
                }
            }
        }
    }
}
