node {
	def application = "springbootapp"
	def dockerImageId = ""

	stage('Clone repository') {
		checkout scm
	}
	

	stage('Build image') {
		app = docker.build("${application}:${BUILD_NUMBER}")
	}

    	stage('Push') {
		docker.withRegistry('https://hub.docker.com/repository/docker', 'DockerHubCredentials') {
           			 app.push("ugaurav22/${application}:${BUILD_NUMBER}")
            			app.push("latest")
       		 }
    	}
	stage('Deploy') {
		sh ("docker run -d -p 81:8080 -v /var/log/:/var/log/ ${application}:${BUILD_NUMBER}")		
	}
	
}
