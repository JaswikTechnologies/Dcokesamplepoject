pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub_id')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            sh 'rm -rf Dcokesamplepoject*'
            sh 'git clone https://github.com/JaswikTechnologies/Dcokesamplepoject.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t jaswiktechnologiesdocker/nodejs:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push jaswiktechnologiesdocker/nodejs:$BUILD_NUMBER'
            }
        }
         stage('Deploy to Docker Host') {
          steps {
            sh    'docker -H tcp://10.1.1.21:2375 stop masterwebapp1 || true'
            sh    'docker -H tcp://10.1.1.21:2375 run --rm -dit --name masterwebapp1 --hostname masterwebapp1 -p 9005:80 jaswiktechnologiesdocker/nodejs:${BUILD_NUMBER}'
            }
        }

        stage('Check WebApp Rechability') {
          steps {
          sh 'sleep 10s'
          sh ' curl http://10.1.1.21:9005'
          }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
