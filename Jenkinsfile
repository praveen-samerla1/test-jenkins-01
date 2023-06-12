pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('Docker_hub')
    
        
    }
    stages { 

        // stage('Build docker image') {
        //     steps {  
                    
        //          sh 'sudo docker build -t praveen0908/sampleapp:9 .'
        //              }
        //          }

        stage('login to dockerhub') {
            steps{
                withCredentials([usernamePassword(credentialsId: 'Docker_hub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    
                 sh '''
                   sudo -S docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
                   sudo docker build -t sampleapp:$BUILD_NUMBER .
                   '''
            }
        }
        }
        stage('push image') {
            steps{
                sh 'sudo docker tag sampleapp praveensamerla/sampleapp:$BUILD_NUMBER'
                sh 'sudo docker push praveensamerla/sampleapp:$BUILD_NUMBER'
            }
        }
    }
   post {
        always {
            sh 'sudo docker logout'
        }
    }

    }

                
