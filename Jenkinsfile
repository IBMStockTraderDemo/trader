pipeline {
    agent any
    stages {
       stage('Build') { 
          steps {
              sh 'mvn clean package' 
          }
       }  
       stage('Deliver') {
            steps {
                sh 'docker build -t trader .'
            }
       }
    }

}