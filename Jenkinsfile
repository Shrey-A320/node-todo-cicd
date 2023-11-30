pipeline {
    
    agent any
    
    stages {
        
        stage("Code"){
          steps{
              git url: "https://github.com/Shrey-A320/node-todo-cicd", branch: "master"
              echo "This is Code stage"
          }  
          
        }   
        stage("build and test"){
            steps{
                sh "docker build -t node-app-test-new ."
                echo "This is build and test stage"
            }
        }   
        stage("Image Scan"){
            steps{
                echo "Docker images scanning"
            }
        }    
        stage("Push"){
           steps{
                withCredentials([usernamePassword(credentialsId: "DockerHub", passwordVariable:"dockerHubPass", usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker tag node-app-test-new:latest ${env.dockerHubUser}/node-app-test-new:latest"
                sh "docker push ${env.dockerHubUser}/node-app-test-new:latest"
                echo "This is push image to repo"
                }
           }
        }    
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo "This is deploy stage"
            }
            
        }   

    }
}
