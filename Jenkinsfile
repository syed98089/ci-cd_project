pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/syed98089/ci-cd_project.git'
             
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
                sh 'docker tag samplewebapp syedkamil/samplewebapp:latest'
                //sh 'docker tag samplewebapp syed/samplewebapp:$BUILD_NUMBER'
               
          }
        }
    

    }
	}
    
