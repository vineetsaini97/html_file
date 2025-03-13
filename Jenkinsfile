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

        stage('kill previous container') {
            steps { 
                sh """
                if
                    "docker rm -f ${container_name}"
                  then
                    ""docker run -d -p 80:80 --name $container_name $image_name"
                fi
                """
            }
        }

        // stage('Run Docker Container') {
        //     steps {
        //             sh "docker run -d -p 80:80 --name $container_name $image_name"
        //     }
        // }
    }
}
