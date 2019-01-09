pipeline {  
    environment {
         componentName = "trader"
         imagename = "${componentName}:${BUILD_NUMBER}"
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
                            componentName: componentName,
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
                                 snapshotName: '$componentName-snapshot-$BUILD_NUMBER'
                             ],
                             deployApp: 'trader',
                             deployDesc: 'Requested from Jenkins',
                             deployEnv: 'DEV 1',
                             deployOnlyChanged: false,
                             deployProc: 'Deploy',
                             deployReqProps: '',
                             deployVersions: 'trader:$BUILD_NUMBER'
                         ],
                         siteName: 'master1'
                     ])
                }
            }
       }
    }
}

