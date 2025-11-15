pipeline {
  agent any
  stages{
    stage('Checkout From Master Branch'){
      steps { 
        git branch: 'master', url: 'https://github.com/praveen-host/docker-test.git'
      }      
    }
  }
}
