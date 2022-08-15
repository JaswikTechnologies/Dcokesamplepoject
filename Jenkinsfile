pipeline {
    agent any
    stages {
        stage("git clone")
        {
            steps{

                sh 'rm -rf Dcokesamplepoject*'
                sh 'git clone https://github.com/JaswikTechnologies/Dcokesamplepoject.git'

            }
            
        }


       stage('Build Docker Image') {
        steps {

	     sh 'cp -r /var/lib/jenkins/workspace/Jenkins-Pipeline/Dcokesamplepoject/* /var/lib/jenkins/workspace/Jenkins-Pipeline'
	     sh 'docker build -t jaswiktechnologiesdocker/nginx:v1 .'   

        }  
	}

	stage('Push Image to Docker Hub') {
        steps {
            sh	'docker push jaswiktechnologiesdocker/nginx:v1'

        }
	}

	stage('Deploy to Docker Host') {
        steps {
            sh	'docker -H tcp://10.1.1.250:2375 run --rm -dit --name webapp1 --hostname webapp1 -p 9000:80 --network ansible_nw jaswiktechnologiesdocker/nginx:v1'

        }
	}

	stage('Check WebApp Rechability') {
        steps{
            sh 'curl http://ec2-13-126-169-104.ap-south-1.compute.amazonaws.com:9000'

        }
	  
	}
    }
}
