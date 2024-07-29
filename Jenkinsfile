pipeline {
  environment {
    imagename = "arntkr13693/c0892298_assignment3_csd4503"
    registryCredential = 'dockerhubaccount'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/arshneetkathuria/NodeExpressAndDocker', branch: 'master'])
 
      }
    }
    stage('Build docker image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }
    stage('Deploy Docker Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
            dockerImage.push('latest')
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imagename:$BUILD_NUMBER"
        sh "docker rmi $imagename:latest"
      }
    }
  }
}