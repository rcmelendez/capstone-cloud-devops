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
    stage('Security Scan') {
      steps { 
        aquaMicroscanner imageName: 'alpine:latest', notCompliesCmd: 'exit 1', onDisallowed: 'fail', outputFormat: 'html'
      }
    }
    stage('Build Docker image') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Test Container') {
      steps {
        sh "docker run -d --rm --name cats -p 8888:5000 $registry:$BUILD_NUMBER"
        script {
          final String url = "http://0.0.0.0:8888"
          final String response = sh(script: "curl -s $url", returnStdout: true).trim()
          echo response
        }
        sh "docker stop cats"
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
    stage('Remove Docker image') {
      steps {
        sh "docker rmi $registry:$BUILD_NUMBER $registry:latest"
      }
    }
    stage('Deploy to AWS EKS cluster') {
      steps {
        sh '''
           kubectl apply -f k8s/namespace.yml
           kubectl apply -f k8s/deployment.yml
           kubectl apply -f k8s/service.yml
           echo "View all resources"
           kubectl get all -o wide -n udacity
           '''
      }
    }
    stage('Rollout Deployment') {
      steps {
        sh '''
           kubectl rollout restart deployment/cats -n udacity
           echo "View all resources"
           kubectl get all -o wide -n udacity
           '''
      }
    }
  }
}
