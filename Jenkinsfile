pipeline {   
  agent any    
  stages {
	  
    stage('Clone repository') {
	    steps {
		checkout scm
	    }	    
     }
    stage('Build Docker Image') {         
      steps{                
	sh 'docker build -t ugaurav22/springbootapp:$BUILD_NUMBER .'           
        echo 'Build Image Completed'                
      }           
    }
    stage('Login to Docker Hub') {         
      steps{ 
	withCredentials([usernamePassword(credentialsId: 'DockerHubCredentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
  		sh 'docker login -u $USERNAME -p $PASSWORD'
	}               
	echo 'Login Completed'                
      }           
    }               
    stage('Push Image to Docker Hub') {         
      steps{                            
	sh ' docker push ugaurav22/springbootapp:$BUILD_NUMBER' 
      echo 'Push Image Completed'       
      }           
    }      
  } //stages 
  post{
    always {  
      sh 'docker logout'           
    }      
  }  
} //pipeline
