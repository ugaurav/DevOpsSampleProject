node {
	def application = "springbootapp"
	

	stage('Clone repository') {
		checkout scm
	}
	
	stage('Assign permission to docker') {
		sh '''
            		#!/bin/bash
            		echo sudo su -;chmod 777 /var/run/docker.sock;exit
         	'''
	}

	stage('Build image') {
		app = docker.build("${application}:${BUILD_NUMBER}")
	}


	stage('Deploy') {
		sh ("docker run -d -p 81:8080 -v /var/log/:/var/log/ ${application}:${BUILD_NUMBER}")
		
	}

	
}
