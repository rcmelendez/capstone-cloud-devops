pipeline {
  environment {
    registry = "rcmelendez/cats"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Lint Dockerfile') {
      steps {
        sh "hadolint Dockerfile"
      }
    }
    stage('Build Docker image') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy image to Docker Hub') {
      steps {
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
            dockerImage.push("latest")
          }
        }
      }
    }
  }
}
