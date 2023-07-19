pipeline {
    agent any

    stages {
        stage('clone') {
            steps {
                echo 'cloning the file'
                git branch: 'main', url: 'https://github.com/LondheShubham153/django-notes-app.git'
             
            }
        }
        stage('deploy') {
            steps {
                echo 'deploy the file'
               sh"docker build -t notes-app ."
               
            }
        }
        stage('push the code ') {
            steps {
                echo 'pusht the image to dockerhub'
               
               withCredentials([usernamePassword(credentialsId: 'Docker-hub', passwordVariable: 'dockerhubpass', usernameVariable: 'dockerhubuser')]) 
               {
    // some block
                 sh"docker tag notes-app ${env.dockerhubuser}/notes-app:latest"
                 sh"docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
                 sh"docker push ${env.dockerhubuser}/notes-app:latest"
                
                }
               
            }
            
            
        }
        stage('Run') {
            steps {
                echo 'deploy the container'
                sh"docker-compose down && docker-compose up -d"
             
            }
        }
        
        
    }
    
}
