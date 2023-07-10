pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    } 

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'sudo docker build -t vkunal/aws-app .'
            }
    }
        stage('Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push') {
            steps {
                sh 'sudo docker push vkunal/aws-app'
            }
        }
        stage('Pull Image & Start Container')
            steps{
                sh 'sudo docker push vkunal/aws-app:latest'
                sh 'docker run -dp 3000:3000 aws-app:latest'
            }

    }
}
