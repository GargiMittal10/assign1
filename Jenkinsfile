pipeline {
    agent {
        docker {
            image 'node:18-alpine'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/GargiMittal10/assign1.git'
            }
        }
        stage('Build & Test') {
            steps {
                sh 'npm install'
                sh 'npm test || echo "No tests"'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t demo-node-app .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d -p 3000:3000 demo-node-app'
            }
        }
    }
}
