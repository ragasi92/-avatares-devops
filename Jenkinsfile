pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }

  environment {
    DOCKERHUB_CREDENTIALS = credentials('RAGASI1992-DOCKERHUB')
  }

  stages {
    stage('Build frontend') {
      steps {
        sh 'docker build -t ragasi1992/avatar-frontend-devops:${env.BUILD_NUMBER} ./web'
        sh 'docker build -t ragasi1992/avatar-backend-devops:${env.BUILD_NUMBER} ./api'
        //sh 'docker build -t ragasi1992/avatar-nginx-devops:latest ./nginx'
      }
    }
    // stage('Build backend') {
    //   steps {
        
    //   }
    //   steps {
    //     sh 'docker build -t ragasi1992/avatar-backend-devops:latest ./api'
    //   }
    // }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push ragasi1992/avatar-frontend-devops'
        sh 'docker push ragasi1992/avatar-backend-devops'
      }
    } 
    //  stage('Push2') {
    //   steps {
    //     sh 'docker push ragasi1992/avatar-backend-devops:latest'
    //   }
    // }
    //  stage('Deploying App to Kubernetes') {
    //   steps {
    //     script {
    //       kubernetesDeploy(configs: "deployment.yml", kubeconfigId: "kubeconfig")
    //     }
    //   }
    // } 

// stage('Deploying App to Kubernetes') {
//       steps {
//         withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: '', contextName: '', 
//         credentialsId: 'SECRET_TOKEN', namespace: '', serverUrl: 'https://54.237.72.127:6443']])  {
//           sh 'curl -LO "https://storage.googleapis.com/kubernetes-release/release/v1.20.5/bin/linux/amd64/kubectl"'  
//           sh 'chmod u+x ./kubectl'  
//           sh './kubectl apply -f deployment.yml'
//           sh './kubectl get nodes'
//       }
//       }
//       }
  }

  post {
    always {
      sh 'docker system prune -f'
      sh 'docker logout'
    }
  }
}