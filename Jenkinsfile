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
				  nexusUrl: '18.138.11.235/:8081', 
				  nexusVersion: 'nexus3', 
				  protocol: 'http', 
				  repository: 'jen-task-03', 
				  version: '${BUILD_NUMBER}'
		  }
	  }
	  	  stage('Pull the Artifact from Nexus and Deploy on Production') {
		  agent{
			  node{
				  label 'jenkins-slave'
			  }
		  }
		  steps {
			  sh 'wget --user=admin --password=cyrilflair@1225'
			  deploy adapters: [
				  tomcat8(credentialsId: 'tomcat', 
					  path: '', 
					  url: 'http://13.213.32.234:8080/')
			  ], 
				  contextPath: '',
				  war: '**/*.war'
		  }
	  }
  }
}
	
	  
