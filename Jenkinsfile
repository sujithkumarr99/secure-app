pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/sujithkumarr99/secure-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t secure-app .'
            }
        }

        stage('Security Scan (Docker Scout)') {
            steps {
                sh 'docker scout quickview secure-app || true'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker run -d -p 5000:5000 --name secure-container secure-app || true
                '''
            }
        }
    }
}