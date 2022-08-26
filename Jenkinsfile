node {
	

	stage('Clone repository') {
		checkout scm
	}

	stage('Build image') {
		app = docker.build("ELKExample")
	}

	stage('Deploy') {
		sh ("docker run -d -p 81:8080 -v /var/log/:/var/log/ ELKExample")
	}
	
	stage('Remove old images') {
		// remove docker pld images
		sh("docker rmi ELKExample:latest -f")
   }
}
