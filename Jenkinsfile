pipeline {
    agent any
    tools { 
        maven
        jdk
    }
    stages {
       stage('Build') { 
          steps {
              sh 'mvn clean package' 
          }
       }  
       stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
       }
    }

}