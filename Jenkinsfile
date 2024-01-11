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
                sh 'sudo docker build . -t srikanth066/docker-nodejs-demo:latest'
            }
        }
        stage('Test image') {
            steps {
                echo 'testing...'
                sh 'sudo docker inspect srikanth066/docker-nodejs-demo:latest '
            }
        }
        
        stage('Push'){
            steps{
        	     sh "sudo docker login -u srikanth066 -p *e+xP%+WtDV.2F+"
                 sh 'sudo docker push srikanth066/docker-nodejs-demo:latest'
            }
        }  
        stage('Deploy'){
            steps{
                echo 'deploying on another server'
                sh 'sudo docker stop srikanth066/docker-nodejs-demo || true'
                sh 'sudo docker rm srikanth066/docker-nodejs-demo || true'
                sh 'whoami'
                sh 'ls -lart /home/jenkins/.ssh'
                sh "ssh -i /home/jenkins/.ssh/id_rsa jenkins@172.31.41.98 'docker pull srikanth066/docker-nodejs-demo'"
                sh "ssh -i /home/jenkins/.ssh/id_rsa jenkins@172.31.41.98 'docker run -d --name dockernodejsdemo -p 8081:8080 srikanth066/docker-nodejs-demo'"
                //sh 'sudo docker run -d --name dockernodejsdemo -p 8000:8000 srikanth066/docker-nodejs-demo:latest'
               // sh '''
                //ssh -i Ubuntudemo.pem -o StrictHostKeyChecking=no ubuntu@ec2-13-235-8-62 <<EOF
                //sudo docker login -u srikanth066 -p *e+xP%+WtDV.2F+
                //sudo docker pull srikanth066/docker-nodejs-demo:latest
                //sudo docker stop dockernodejsdemo || true
                //sudo docker rm dockernodejsdemo || true 
                //sudo docker run -d --name dockernodejsdemo -p 8000:8000 srikanth066/docker-nodejs-demo:latest
                //EOF
                //'''
            }
        }
    }
}
