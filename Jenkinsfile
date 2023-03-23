node {
	def application = "springbootapp"
	def dockeruser = "ugaurav22"
	environment {
    		DOCKERHUB_CREDENTIALS = credentials('DockerHubCredentials')
  	}
	stage('Clone repository') {
		checkout scm
	}
	

	stage('Build image') {
		//app = docker.build("${application}:${BUILD_NUMBER}")
		sh 'docker build -t ugaurav22/springbootapp:${BUILD_NUMBER} .'	
	}

    	stage('Push') {
		/*docker.withRegistry('https://hub.docker.com/repositories/', 'DockerHubCredentials') {
           			 app.push("ugaurav22/${application}:${BUILD_NUMBER}")
            			app.push("latest")
       		 }
		dockerImage = docker.build registry + ":$BUILD_NUMBER"
		script {
			docker.withRegistry( 'https://hub.docker.com/repository/docker/ugaurav22/', registryCredential ) {
			app.push("ugaurav22/${application}:${BUILD_NUMBER}")
				app.push("latest")
			}
    		}*/
		sh 'docker logout'
		sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
		/*withDockerRegistry([credentialsId:"DockerHubCredentials",url:"https://index.docker.io/v2/"]) {
           		//sh 'docker tag springbootapp:${BUILD_NUMBER} ugaurav22/springbootapp:${BUILD_NUMBER}'	
			//sh 'docker push ugaurav22/springbootapp:${BUILD_NUMBER}'

       		 }*/
		sh 'docker push ugaurav22/springbootapp:${BUILD_NUMBER}'
	}	
	stage('Deploy') {
		sh ("docker run -d -p 81:8080 -v /var/log/:/var/log/ ${application}:${BUILD_NUMBER}")		
	}
	
}
