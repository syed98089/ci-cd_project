pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
     }
     environment {
        AWS_ACCOUNT_ID="182130711581"
        AWS_DEFAULT_REGION="us-east-1" 
        IMAGE_REPO_NAME="my_ecr_repo"
        IMAGE_TAG="latest"
        REPOSITORY_URI = "182130711581.dkr.ecr.us-east-1.amazonaws.com/my_ecr_repo"
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
          }
        }
    
    stage('Logging into AWS ECR') {
            steps {
                script {
                sh " aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 182130711581.dkr.ecr.us-east-1.amazonaws.com"
              }
                 
            }
        }
   // Building Docker images
    stage('Building image') {
      steps{
        script {
          dockerImage = docker build -t my_ecr_repo .
        }
      }
    }

// Uploading Docker images into AWS ECR
    stage('Pushing to ECR') {
     steps{  
         script {
                sh "docker tag my_ecr_repo:latest 182130711581.dkr.ecr.us-east-1.amazonaws.com/my_ecr_repo:latest"
                sh "docker push 182130711581.dkr.ecr.us-east-1.amazonaws.com/my_ecr_repo:latest"
         }
        }
      }

    }
	}
    
