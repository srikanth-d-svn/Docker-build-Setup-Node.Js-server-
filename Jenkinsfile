pipeline {
    agent any
    stages {
        stage("code"){
            steps{
                git url: "https://github.com/srikanth-d-svn/Docker-build-Setup-Node.Js-server-.git", branch: "master"  
            }
        }
        stage("build and test"){
            steps{
                sh "docker build -t node-app-test-new ."  
            }
        }
        stage("scan image"){
            steps{  
            }
        }
        stage("push"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker tag node-app-test-new:latest ${env.dockerHubUser}/node-app-test-new:latest"
                sh "docker push ${env.dockerHubUser}/node-app-test-new:latest"
                }
            }
        }
        stage("deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d" 
            }
        }
    }
}
