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
        
        stage('Kill Previous Container') {
            steps {
                       sh "docker stop $container_name" 
                       sh "docker rm -f $container_name"          
            }
        }

        stage('Build Docker Image') {
            steps {                
                    sh "docker build -t $image_name ."            
            }
        }

        stage('Run Docker Container') {
            steps {
                    sh "docker run -d -p 80:80 --name $container_name $image_name"
            }
        }
    }
}
