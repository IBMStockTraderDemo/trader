pipeline {  
    environment {
         component = "trader"
         imagename = "${component}:${BUILD_NUMBER}"
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
            steps {
                script {
                    step([$class: 'UCDeployPublisher',
                        component: [
                            componentName: '${component}',
                            componentTag: '',
                            delivery: [
                                $class: 'Push',
                                baseDir: pwd(),
                                fileExcludePatterns: '',
                                fileIncludePatterns: 'manifests/deploy.yaml',
                                pushDescription: '',
                                pushIncremental: false,
                                pushProperties: '',
                                pushVersion: '${BUILD_NUMBER}'
                            ]
                         ],
                         deploy: [
                             createSnapshot: [
                                 deployWithSnapshot: true,
                                 snapshotName: '${component}-snapshot-${BUILD_NUMBER}'
                             ],
                             deployApp: '${component}',
                             deployDesc: 'Requested from Jenkins',
                             deployEnv: 'DEV 1',
                             deployOnlyChanged: false,
                             deployProc: 'Deploy',
                             deployReqProps: '',
                             deployVersions: '${component}:${BUILD_NUMBER}'
                         ],
                         siteName: 'master1'
                     ])
                }
            }
       }
    }
}

