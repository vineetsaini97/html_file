pipeline{
    agent any
    stages{
        environment('name'){
             image_name='nginx-image'
             container_name='pipeline-container'    
           }
        }
         stage('kill previuos container'){
             steps{
                 // kill the previous container
               sh """
                  if docker ps -a --filter name=${container_name} -q; 
                  then
                  docker rm -f ${container_name}
                  fi
                 """
           }
         }
         stage('Build Docker Image') {
            steps {
                // Build Docker image using the Dockerfile
                sh 'docker build -t nginx-image .'
            }
        }
        stage('Run Docker Container') {
            steps {
                // Run the Docker container using the newly built image
                sh 'docker run -d -p 80:80 --name pipeline-container nginx-image'
            }
        }
    }
}

