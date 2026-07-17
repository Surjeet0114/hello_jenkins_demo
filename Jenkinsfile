pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Maven Project') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t hello-app:latest .'
            }
        }

        stage('Push Docker Image to ECR') {

            steps {

                sh '''
                    docker tag hello-app:latest 323336951226.dkr.ecr.ap-south-1.amazonaws.com/hello-app:latest

                    export AWS_PAGER=""
                    aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 323336951226.dkr.ecr.ap-south-1.amazonaws.com
                    docker push 323336951226.dkr.ecr.ap-south-1.amazonaws.com/hello-app:latest
                '''
            }
        }

        stage('Deploy to EC2') {
            steps {
                echo 'Deploying Application to EC2...'
            }
        }
    }
}