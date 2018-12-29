pipeline {  
    environment {
         registry = "trader"
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
                sh 'ibmcloud target -o kacz@us.ibm.com -s dev && ibmcloud cr login '
                script {
                    docker.build registry
                }
                sh 'ibmcloud cr login'
                sh 'docker tag trader registry.ng.blumix.net/kacz/trader'
                sh 'docker push registry.ng.blumix.net/kacz/trader'
            }
       }
    }

}