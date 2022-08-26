node {
	

	stage('Clone repository') {
		checkout scm
	}

	stage('Build image') {
		app = docker.build("elkexample")
	}

	stage('Deploy') {
		sh ("docker run -d -p 81:8080 -v /var/log/:/var/log/ elkexample")
	}
	
	stage('Remove old images') {
		// remove docker pld images
		sh("docker rmi elkexample:latest -f")
   }
}
