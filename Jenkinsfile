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
                sh 'ibmcloud target -r us-south'
                sh 'echo 5 | ibmcloud login --apikey GZQdst5w6DkMgMenHLvq-pOeMnMjMm0mCS4R2BPTKGye'
                sh 'ibmcloud target -o kacz@us.ibm.com -s dev'
                script {
                    docker.build registry
                }
            }
       }
    }

}