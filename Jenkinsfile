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
                script {
                    docker.build registry
                }
                sh '/push2cloud.sh trader'
            }
       }
    }

}