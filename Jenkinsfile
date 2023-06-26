pipeline {
  environment {
    dockerimagename = "rupeshsaini09/intern-webapp"
    dockerImage = ""
  }
  agent any
  stages {
    stage('Checkout Source') {
      steps {
        git 'https://github.com/rupeshsaini09/intern-webapp.git'
      }
    }
    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }
    stage('Pushing Image') {
      environment {
               registryCredential = 'docker-hub-creds'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }
    stage('Deploying webapp to Kubernetes') {
      steps {
        script {
          sh "ls"
          sh 'kubectl apply -f deploy.yml'
          sh "pwd"
          sh "ip a"
        }
      }
    }
  }
}
