pipeline {
    agent any
    stages {
        stage("git clone")
        {
            sh 'rm -rf Dcokesamplepoject*'
            sh 'git clone https://github.com/JaswikTechnologies/Dcokesamplepoject.git'
        }
        stage("QED")
        {
            steps {
                echo "-----------------------"
                echo "QEDDD"
            }
        }
        stage("PROD")
        {
            steps {
                echo "-----------------------"
                echo "PRODD"
            }
        }
        
    }
}
