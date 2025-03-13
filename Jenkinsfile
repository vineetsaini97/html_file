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
                    echo "Image Name: $image_name"
                    echo "Container Name: $container_name"
                }
            }
        }
        
        stage('build docker image') {
            steps {
                   sh "docker build -t $image_name ."
            }
        }

       stage('Kill previous container') {
    steps {
        script {
            // Check if the container exists
            def containerExists = sh(script: "docker ps -a --filter name=${container_name} -q", returnStdout: true).trim()

            if (containerExists) {
                // If the container exists, remove it
                sh "docker rm -f ${container_name}"
            } else {
                // If the container doesn't exist, run a new container
                sh "docker run -d -p 80:80 --name ${container_name} ${image_name}"
            }
        }
      } 
    }
 }
}
                    
