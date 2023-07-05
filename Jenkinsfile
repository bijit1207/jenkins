pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=bijit1207 -Dsonar.organization=bijit1207 -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=45332fbe8142d43c16c3f2945ca7c6aa9f4f599b'
			}
        } 

    post {
        always {
            archiveArtifacts artifacts: '*',
        }
    }
    
    stage('Publish SonarCloud Logs to Artifactory') {
            steps {
                script {
                    // Configure Artifactory details
                    def server = Artifactory.server('artifactory')

                    // Define the Artifactory upload specification for SonarCloud logs
                    def uploadSpec = """
                        {
                            "files": [
                                {
                                    "pattern": "*/.zip",
                                    "target": "https://bijitjfrog1207.com/artifactory/maven/"
                                }
                            ]
                        }
                    """

                    // Upload SonarCloud logs to Artifactory
                    server.upload(uploadSpec)
                }
            }
        }
  }
}
