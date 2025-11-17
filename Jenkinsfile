pipeline {
  agent any
  environment {
    DOCKER_IMAGE = "yadavpk/minimalwebapi"
    DOCKER_TAG = "latest"
    DOCKER_CREDENTIALS=credentials('dockerhub-creds')
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
    stage('Login to dockerhub'){
      steps{
        sh "docker login --username ${DOCKER_CREDENTIALS_USR} --password ${DOCKER_CREDENTIALS_PSW}"
      }
    }

  }
}
