pipeline {


    options {
        buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '5'))
    }
    agent any

    tools {
        maven 'maven_3.0.5'
    }

    stages {
        stage('Code Compilation') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
           steps {
                sh 'docker build -t newonetwo .'
           }
         }
        stage('Upload Docker Image to AWS ECR') {
                    steps {
        			   script {
        			      withDockerRegistry([credentialsId:'ecr:ap-south-1:best-ecr', url:"https://041052185687.dkr.ecr.ap-south-1.amazonaws.com"]){
                          sh """
        				  echo "Tagging the Docker Image: In Progress"
        				  docker tag newone:latest 041052185687.dkr.ecr.ap-south-1.amazonaws.com/newonetwo:latest
        				  echo "Tagging the Docker Image: Completed"
        				  echo "Push Docker Image to ECR : In Progress"
        				  docker push 041052185687.dkr.ecr.ap-south-1.amazonaws.com/newonetwo:latest
        				  echo "Push Docker Image to ECR : Completed"
        				  """
        				  }
        				  }
                        }
                    }
        stage('Deploy to Production') {
                    steps {
                        sh 'date'
                    }
                }
             }
}