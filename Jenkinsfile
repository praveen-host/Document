pipeline {
  agent any
  environment {
    DOCKER_IMAGE = "yadavpk/minimalwebapi"
    DOCKER_TAG = "latest"
  }

  stages{
    stage('Checkout From Master Branch'){
      steps { 
        git branch: 'master', url: 'https://github.com/praveen-host/WebAPI001.git'
      }      
    }
    stage('Docker Build') {
      steps {
        sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
      }
    }

  }
}
