pipeline {
  agent any
  environment {
    DOCKER_IMAGE = "yadavpk/minimalwebapi"
    DOCKER_TAG = "latest"
  }

  stages{
    stage('Checkout From Master Branch'){
      steps { 
        git branch: 'master', url: 'https://github.com/praveen-host/docker-test.git'
      }      
    }
    stage('Docker Build') {
      steps {
        sh "docker build -f .github/workflows/docker-image.yml -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
      }
    }

  }
}
