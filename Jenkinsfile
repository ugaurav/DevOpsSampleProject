node {
	def application = "springbootapp"
	def dockeruser = "ugaurav22"
	environment {
			registry = "https://hub.docker.com/repository/docker/ugaurav22/"
			registryCredential = 'DockerHubCredentials'
			dockerImage = ''
	}
	stage('Clone repository') {
		checkout scm
	}
	

	stage('Build image') {
		app = docker.build("${application}:${BUILD_NUMBER}")
	}

    	stage('Push') {
		/*docker.withRegistry('https://hub.docker.com/repositories/', 'DockerHubCredentials') {
           			 app.push("ugaurav22/${application}:${BUILD_NUMBER}")
            			app.push("latest")
       		 }*/
		dockerImage = docker.build registry + ":$BUILD_NUMBER"
		script {
			docker.withRegistry( 'https://hub.docker.com/repository/docker/ugaurav22/', registryCredential ) {
			app.push("ugaurav22/${application}:${BUILD_NUMBER}")
				app.push("latest")
			}
    		}
	}	
	stage('Deploy') {
		sh ("docker run -d -p 81:8080 -v /var/log/:/var/log/ ${application}:${BUILD_NUMBER}")		
	}
	
}
