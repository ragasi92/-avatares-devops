pipeline {
  agent { label 'principal' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('RAGASI1992-DOCKERHUB')
  }
  stages {
    stage('Build frontend') {
      steps {
        sh 'docker build -t ragasi1992/avatar-frontend-devops:latest ./web'
      }
    }
    stage('Build backend') {
      steps {
        sh 'docker build -t ragasi1992/avatar-backend-devops:latest ./api'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push ragasi1992/avatar-frontend-devops:latest'
      }
    }
     stage('Push2') {
      steps {
        sh 'docker push ragasi1992/avatar-backend-devops:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}