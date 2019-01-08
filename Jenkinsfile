pipeline {  
    environment {
         imagename = "trader:$BUILD_NUMBER"
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
                    docker.build imagename
                }
                sh '/push2dockerhub.sh $imagename'
            }
       }
       stage('UCD Deploy') {
            def PWD = pwd();
            steps {
                script {
                    step([$class: 'UCDeployPublisher',
                        component: [
                            componentName: 'trader',
                            componentTag: '',
                            delivery: [
                                $class: 'Push',
                                baseDir: pwd(),
                                fileExcludePatterns: '',
                                fileIncludePatterns: 'manifests/deploy.yaml',
                                pushDescription: '',
                                pushIncremental: false,
                                pushProperties: '',
                                pushVersion: '$BUILD_NUMBER'
                            ]
                         ],
                         deploy: [
                             createSnapshot: [
                                 deployWithSnapshot: true,
                                 snapshotName: 'trader-snapshot-$BUILD_NUMBER'
                             ],
                             deployApp: 'trader',
                             deployDesc: 'Requested from Jenkins',
                             deployEnv: 'DEV',
                             deployOnlyChanged: false,
                             deployProc: 'Deploy',
                             deployReqProps: '',
                             deployVersions: ''
                         ],
                         siteName: 'master1'
                     ])
                }
            }
       }
    }
}

