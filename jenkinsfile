pipeline {
    agent any
    stages {
        stage('Copy File') {
            steps {
                // Example command to copy files
                sh 'cp /index.html /usr/share/nginx/html'
            }
        }
        stage('Build Docker Image') {
            steps {
                // Build Docker image using the Dockerfile
                sh 'docker build -t my-nginx-image .'
            }
        }
        stage('Run Docker Container') {
            steps {
                // Run the Docker container using the newly built image
                sh 'docker run -d -p 80:80 my-nginx-image'
            }
        }
    }
}
