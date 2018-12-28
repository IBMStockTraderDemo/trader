pipeline {
    agent any
    tools { 
        maven 'maven 3'
        jdk 'java 8'
    }
    stages {
      stage ("initialize") {
        steps {
          sh '''
          echo "PATH = ${PATH}"
          echo "M2_HOME = ${M2_HOME}"
          '''
       }
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