pipeline {
  environment {
    registry = "anthonyto01/cw2"
    registryCredential = 'dockerhub'
    dockerImage = 'hub.docker.com/repository/docker/ato204/cw2'
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/anthonyto01/cw2/tree/main'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
  }
}
