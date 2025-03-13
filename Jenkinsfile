pipeline {
    agent any
    environment {
        image_name = 'nginx-image'
        container_name = 'pipeline-container'
      }
    stages {
       stage('Environment Setup') {
            steps {
                script {
                    echo "Image Name: ${image_name}"
                    echo "Container Name: ${container_name}"
                 }
              }
           }
        }
       stage('kill previuos container') {
            steps{
                 // kill the previous container
                 script {
                  sh """
                    if docker ps -a --filter name=${container_name} -q; 
                    then
                    docker rm -f ${container_name}
                    fi 
                    """
                  }
              }      
           }
       stage('Build Docker Image') {
           steps {
                // Build Docker image using the Dockerfile
                 script{
                  sh 'docker build -t ${nginx-image} .'
                }
            }
        }
      stage('Run Docker Container') {
            steps {
                // Run the Docker container using the newly built image
                script{
                  sh 'docker run -d -p 80:80 --name ${pipeline-container} ${nginx-image}'
                }
            }
        }
    }
