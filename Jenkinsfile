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
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
            sh """
                echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
            """
        }        
      }
    }
    stage('Push image to docker hub'){
      steps{
        sh "docker push ${DOCKER_IMAGE}:${DOCKER_TAG}"      
      }      
    }
    stage('Azure Login') {
      steps {
        sh 'az login --identity' // or use Service Principal
      }
    }
    stage('Get AKS Credentials'){
      steps{
        sh "az aks get-credentials --resource-group CICD_RGroup --name Jenkins-AKS --overwrite-existing"
      } 
    }
    stage('HelloWorld'){
      steps{
        sh 'kubectl run helloworld --image=yadavpk/helloworld:1.0.1 --port=8080'
      }
    }
    stage('Get AKS Pods'){
      steps{
        sh 'kubectl get pods'
      }
    }
  }
}
