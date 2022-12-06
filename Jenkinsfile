pipeline {
  agent {
    node {
      label 'jenkins-slave'
    }
  }
  stages{
	stage(" Maven Build"){
		steps{
			sh 'mvn clean package'
		}
            }
        stage("Quality Check"){
		steps{
			withSonarQubeEnv('SonarQube') {
				sh "mvn sonar:sonar"
			}
		}
      }
	stage("Upload to Nexus"){
		  steps{
			  nexusArtifactUploader artifacts: [
				  [
					  artifactId: 'DevOpsDemo', 
					  classifier: '', 
					  file: 'target/DevOpsDemo.war', 
					  type: 'war'
				  ]
			  ],
				  credentialsId: 'nexus', 
				  groupId: 'com.blazeclan', 
				  nexusUrl: '13.214.121.130:8081', 
				  nexusVersion: 'nexus3', 
				  protocol: 'http', 
				  repository: 'jen-task-03', 
				  version: '1.${BUILD_NUMBER}'
		  }
	  }
  }
}
