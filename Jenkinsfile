pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }

  environment {
    DOCKERHUB_CREDENTIALS = credentials('DOCKERHUB')
  }

  stages {
    stage('Build frontend') {
      steps {
        sh "docker build -t ragasi1992/avatar-frontend-devops:${env.BUILD_NUMBER} ./web"
        sh "docker build -t ragasi1992/avatar-backend-devops:${env.BUILD_NUMBER} ./api"
      }
    }

    stage('Login') {
      when {
          branch "main"
      }
      steps {
        sh 'docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      when {
          branch "main"
      }
      steps {
        sh "docker push ragasi1992/avatar-frontend-devops:${env.BUILD_NUMBER}"
        sh "docker push ragasi1992/avatar-backend-devops:${env.BUILD_NUMBER}"
      }
    } 

    stage('Trigger ManifestUpdate') {
      when {
          branch "main"
      }
        steps {
            echo "triggering updatemanifestjob"
            build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }        
    }
  }

  post {
    always {
      sh 'docker system prune -f'
      sh 'docker logout'
    }
  }
}