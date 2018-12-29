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
                sh 'ibmcloud login --apikey @ibmcloudapi.key --check-version=false'
                script {
                    docker.build registry
                }
            }
       }
    }

}