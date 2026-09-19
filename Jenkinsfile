pipeline {
    agent any

    environment {
        PATH = "/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t lab11-nodejs .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                    docker rm -f lab11-container || true
                    docker run -d -p 3001:3000 --name lab11-container lab11-nodejs
                '''
            }
        }

        stage('Verify API') {
            steps {
                sh 'curl -f http://localhost:3001/status'
            }
        }
    }
}