pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/sujithkumarr99/secure-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t secure-app .'
            }
        }

        stage('Security Scan (Docker Scout)') {
            steps {
                bat 'docker scout quickview secure-app || true'
            }
        }

        stage('Run Container') {
            steps {
                bat '''
                docker run -d -p 5000:5000 --name secure-container secure-app || true
                '''
            }
        }
    }
}