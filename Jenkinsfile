pipeline {
    agent none
    environment {
        imageName = 'sommaik/my_web_ex'
        port = 80
    }
    
    stages {
       stage('Package') { 
          agent any
          steps {
              sh "docker --version"
              sh "docker build -t ${imageName} ."
            withCredentials(
                [usernamePassword(credentialsId: 'docker_hub', 
                passwordVariable: 'dockerHubPassword', 
                usernameVariable: 'dockerHubUser')]) {
              sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
              sh "docker push ${imageName}"
            }
          }
       }

       stage('Deploy') { 
          agent {label 'mgr1'}
          steps {
           sh "echo h"
          }
       }
    }
}