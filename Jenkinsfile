pipeline {   
  agent any  
  environment {     
    DOCKERHUB_CREDENTIALS= credentials('DockerHubCredentials')     
  }    
  stages {         
    stage('Clone repository') {
	    steps {
		checkout scm
	    }	    
     }
    stage('Build Docker Image') {         
      steps{                
	sh 'sudo docker build -t ugaurav22/springbooapp:$BUILD_NUMBER .'           
        echo 'Build Image Completed'                
      }           
    }
    stage('Login to Docker Hub') {         
      steps{                            
	sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'                 
	echo 'Login Completed'                
      }           
    }               
    stage('Push Image to Docker Hub') {         
      steps{                            
	sh 'sudo docker push ugaurav22/springbooapp:$BUILD_NUMBER' 
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
