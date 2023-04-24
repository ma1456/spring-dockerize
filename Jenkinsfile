pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ma1456/spring-dockerize.git']])
            }
        }
       stage ("build Jar") {
            steps {
                sh "/opt/maven/bin/mvn clean package"
            }
        }
	stage('Upload'){
            steps{
                rtUpload (
                 serverId:"jfrog" ,
                  spec: '''{
                   "files": [
                      {
                      "pattern": "*.jar",
                      "target": "maven-local-repo/"
                      }
                            ]
                           }''',
                        )
               }
         }
	stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "jfrog"
                 )
                }
            }
       
        }
  }
