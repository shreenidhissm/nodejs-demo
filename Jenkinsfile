pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker_login')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/shreenidhissm/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t shreenidhism/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to docker hub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push shreenidhism/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

