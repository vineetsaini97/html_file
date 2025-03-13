pipeline {
    agent docker
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
        
        stage('Kill Previous Container') {
            steps {
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
                    sh "docker build -t ${image_name} ."            
            }
        }

        stage('Run Docker Container') {
            steps {
                    sh "docker run -d -p 80:80 --name ${container_name} ${image_name}"
            }
        }
    }
}
