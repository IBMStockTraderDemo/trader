pipeline {
    agent any
    tools { 
        maven 'maven 3'
        jdk 'java 8'
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