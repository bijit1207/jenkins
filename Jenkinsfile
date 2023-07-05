pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {			  
		sh 'mvn clean verify -l sonar/log.txt sonar:sonar -Dsonar.projectKey=jenkins-sonar-ci_pipeline -Dsonar.organization=jenkins-sonar-ci -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=6b97f056496f86ba20857ab4349e4ae20fd980a1'
		}           
      } 

    stage ('Artifactory configuration') {
            steps {
                rtServer (
                    id: "artifactory",
                    url: "https://rdevsecops64.jfrog.io",
                    credentialsId: admin
                )

                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: "artifactory",
                    releaseRepo: "https://rdevsecops64.jfrog.io/artifactory/api/maven/maven-libs-release",
                    snapshotRepo: "https://rdevsecops64.jfrog.io/artifactory/api/maven/maven-libs-snapshot"
                )

                rtMavenResolver (
                    id: "MAVEN_RESOLVER",
                    serverId: "artifactory",
                    releaseRepo: "https://rdevsecops64.jfrog.io/artifactory/api/maven/maven-libs-release",
                    snapshotRepo: "https://rdevsecops64.jfrog.io/artifactory/api/maven/maven-libs-snapshot"
                )
            }
        }
  }
}
