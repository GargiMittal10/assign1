pipeline {
  agent any
  environment {
    IMAGE_NAME = "jenkins-docker-demo"
    CONTAINER_NAME = "jenkins-docker-demo-container"
  }
  stages {
    stage('Checkout') {
      steps { checkout scm }
    }
    stage('Build & Test') {
      steps {
        sh 'npm install'
        sh 'npm test'
      }
    }
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t $IMAGE_NAME:$BUILD_NUMBER .'
      }
    }
    stage('Deploy') {
      steps {
        sh 'docker rm -f $CONTAINER_NAME || true'
        sh 'docker run -d --name $CONTAINER_NAME -p 3000:3000 $IMAGE_NAME:$BUILD_NUMBER'
      }
    }
  }
}
