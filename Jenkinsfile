pipeline {
  agent any

  stages {
    stage('Build Docker Image') {
      steps {
        script {
          dockerApp = docker.build("andrrade/guia-jenkins:${env.BUILD_ID}", "-f ./src/Dockerfile ./src")
        }
      }
    }
    
    stage('Push Docker Image') {  
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
            dockerApp.push('latest')
            dockerApp.push("${env.BUILD_ID}")
          }
        }
      }
    }
    
    stage('Deploy no Kubernetes') {
      steps {
        sh 'echo "Executando o comando kubectl apply"'
      }
    }
  }
}
