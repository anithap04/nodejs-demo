pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-password')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/anithap04/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t sampledocker546/nodeappnew:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push sampledocker546/nodeappnew:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

