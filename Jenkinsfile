pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                deleteDir()
                git branch: 'main', url: 'https://github.com/sujithkumarr99/secure-app.git'
            }
        }

        stage('Build & Deploy') {
            steps {
                bat '''
                docker rm -f secure-container 2>nul
                docker build --no-cache -t secure-app .
                docker run -d -p 5000:5000 --name secure-container secure-app
                '''
            }
        }

        stage('Security Scan') {
            steps {
                bat 'docker scout quickview secure-app'
            }
        }
    }
}