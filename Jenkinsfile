pipeline {
    agent any 
   
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/nushan2000/3920-Ediriwickrama.git'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t nushan2000/nodeapp-cuban:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'samin-docker', variable: 'samindocker')]) {
   
               bat'docker login -u nushan2000 -p ${nushandocker}'
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push nushan2000/nodeapp-cuban:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}
