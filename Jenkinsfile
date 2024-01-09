pipeline {
    agent any
    stages{
        stage('Checkout'){
            steps{
                git url: 'https://github.com/srikanth-d-svn/Docker-build-Setup-Node.Js-server-.git', branch: 'main'
            }
        }
        stage('Build'){
            steps{
                sh 'sudo docker build . -t srikanth066:latest'
            }
        }
        stage('Test image') {
            steps {
                echo 'testing...'
                sh 'sudo docker inspect --type=image srikanth066:latest '
            }
        }
        
        stage('Push'){
            steps{
        	     sh "sudo docker login -u srikanth -p dckr_pat_OvN0lH_USJztUCkm0opyjz-yXNc"
                 sh 'sudo docker push srikanth066:latest'
            }
        }  
        stage('Deploy'){
            steps{
                echo 'deploying on another server'
                sh 'sudo docker stop srikanth066 || true'
                sh 'sudo docker rm srikanth066 || true'
                sh 'sudo docker run -d --name nodetodoapp srikanth066:latest'
                sh '''
                ssh -i Ubuntudemo.pem -o StrictHostKeyChecking=no ubuntu@44.211.144.201 <<EOF
                sudo docker login -u srikanth -p dckr_pat_OvN0lH_USJztUCkm0opyjz-yXNc
                sudo docker pull srikanth066:latest
                sudo docker stop nodetodoapp || true
                sudo docker rm nodetodoapp || true 
                sudo docker run -d --name nodetodoapp srikanth066:latest
                '''
            }
        }
    }
}
