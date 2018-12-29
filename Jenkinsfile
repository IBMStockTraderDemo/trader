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
                sh 'ibmcloud config  --check-version=false'
                sh 'ibmcloud login --apikey @ibmcloudapi.key'
                sh 'ibmcloud target -o kacz@us.ibm.com -s dev'
                script {
                    docker.build registry
                }
            }
       }
    }

}