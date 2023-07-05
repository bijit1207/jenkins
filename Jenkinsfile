pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
        sh 'mvn clean verify -s setting.xml sonar:sonar -Dsonar.projectKey=bijit1207 -Dsonar.organization=bijit1207 -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=45332fbe8142d43c16c3f2945ca7c6aa9f4f599b'
			}       
        }
    }
}
