pipeline {  
    environment {
         registry = "trader"
         registryCredential = 'dockerhub'
     }

    agent any
    stages {
       stage('Build') { 
          steps {
              sh 'mvn clean package' 
          }
       }  
       stage('Deliver') {
            steps {
                script {
                    docker.build registry
                }
            }
       }
    }

}