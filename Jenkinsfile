
pipeline {

environment{
dockerimage = ""
}

    agent any

  stages {

    stage('Checking Git for Dockerfile') {
      steps {
        checkout scm
      }
    }
    
      stage("Build Docker Image") {
            steps {
                script {
                    dockerimage = docker.build("ato204/cw2")
                }
            }
        }
	
      stage("Push Docker Image") {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', '1369c73d-2700-4fc2-9454-f0718e2b7c69') {
                            dockerimage.push("latest")
                            dockerimage.push("${env.BUILD_ID}")
                    }
                }
            }
        }

    
    stage('Test Container / Build Test') {
      steps {
        sh 'docker run --detach --publish 80:80 --name cw2 ato204/cw2'
        }
      }
    }

  }

