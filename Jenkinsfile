pipeline {

    agent any

    tools {
        maven 'Maven'
        jdk 'Java17'
    }

    environment {
        COMPOSE_PROJECT_NAME = "payment-system"
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/YOUR_GITHUB_USERNAME/payment-integration-system-project.git'
            }
        }

        stage('Build All Microservices') {
            steps {

                dir('payment-validation-service') {
                    sh 'mvn clean package -DskipTests'
                }

                dir('payment-processing-service') {
                    sh 'mvn clean package -DskipTests'
                }

                dir('stripe-provider-service') {
                    sh 'mvn clean package -DskipTests'
                }

            }
        }

        stage('Docker Compose Build') {
            steps {
                sh 'docker compose build'
            }
        }

        stage('Run Containers') {
            steps {
                sh 'docker compose down || true'
                sh 'docker compose up -d'
            }
        }

        stage('Check Running Containers') {
            steps {
                sh 'docker ps'
            }
        }

    }

}