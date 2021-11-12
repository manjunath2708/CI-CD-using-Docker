pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/manjunath2708/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
              
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp bane92ng/samplewebapp:latest'
                //sh 'docker tag samplewebapp bane92ng/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "https://hub.docker.com/repository/docker/bane92ng/samplewebapp" ]) {
          sh  'docker push bane92ng/samplewebapp:latest'
        //  sh  'docker push bane92ng/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 bane92ng/samplewebapp"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 8003:8080 /samplewebapp"
 
            }
        }
    }
	}
    
