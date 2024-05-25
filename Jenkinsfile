pipeline {
  agent { label 'principal' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('RAGASI1992-DOCKERHUB')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t ragasi1992/avatar-backend-devops:latest ./api'
      }
      steps {
        sh 'docker build -t ragasi1992/avatar-frontend-devops:latest ./web'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push ragasi1992/avatar-backend-devops:latest'
      }
      steps {
        sh 'docker push ragasi1992/avatar-frontend-devops:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}