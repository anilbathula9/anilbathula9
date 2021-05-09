pipeline {
  environment {
    registry = "anil79/springboot"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }    
  agent any
  tools {maven "maven363" }
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/anilbathula9/spring-boot-hello-world.git'
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
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
        sh "docker run -d --name Inspiredit9 -p 8089:8080 cloudsofthyd/springboot:$BUILD_NUMBER"
        
      }
    }     
      }
   }
