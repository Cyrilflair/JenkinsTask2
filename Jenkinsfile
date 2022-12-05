pipeline {
  agent {
    node {
      label 'Jenkins-Slave'
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
				  nexusUrl: '13.213.14.6:8081', 
				  nexusVersion: 'nexus3', 
				  protocol: 'http', 
				  repository: 'Jenkins-task-3', 
				  version: '1.${BUILD_NUMBER}'
		  }
	  }
  }
}
