pipeline {

environment{
dockerimage = ""
}

    agent any

  stages {

    stage('Checkout Git') {
      steps {
        checkout scm
      }
    }
    
      stage("Build Docker Image") {
            steps {
                script {
                    myapp = docker.build("ato204/cw2:${env.BUILD_ID}")
                }
            }
        }
    
      stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }

    
    stage('Deploy App') {
      steps {
        sh 'docker run --detach --publish 80:80 --name cw2 ato204/cw2'
        }
      }
    }

  }

