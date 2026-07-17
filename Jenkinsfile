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
                echo 'Building Maven Project...'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker Image...'
            }
        }

        stage('Push Docker Image to ECR') {
            steps {
                echo 'Pushing Image to Amazon ECR...'
            }
        }

        stage('Deploy to EC2') {
            steps {
                echo 'Deploying Application to EC2...'
            }
        }
    }
}