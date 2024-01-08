pipeline {
    agent { label 'Dev-Agent node' }
    
    stages{
        stage('Checkout'){
            steps{
                git url: 'https://github.com/srikanth-d-svn/Docker-build-Setup-Node.Js-server-.git', branch: 'main'
            }
        }
        stage('Build'){
            steps{
                sh 'sudo docker build . -t srikanth/nodo-todo-app-test:latest'
            }
        }
        stage('Test image') {
            steps {
                echo 'testing...'
                sh 'sudo docker inspect --type=image srikanth/nodo-todo-app-test:latest '
            }
        }
        
        stage('Push'){
            steps{
        	     sh "sudo docker login -u srikanth -p dckr_pat_OvN0lH_USJztUCkm0opyjz-yXNc"
                 sh 'sudo docker push srikanth/nodo-todo-app-test:latest'
            }
        }  
        stage('Deploy'){
            steps{
                echo 'deploying on another server'
                sh 'sudo docker stop nodetodoapp || true'
                sh 'sudo docker rm nodetodoapp || true'
                sh 'sudo docker run -d --name nodetodoapp srikanth/nodo-todo-app-test:latest'
                sh '''
                ssh -i Ubuntudemo.pem -o StrictHostKeyChecking=no  ubuntu@ec2-13-233-25-81 <<EOF
                sudo docker login -u srikanth -p dckr_pat_OvN0lH_USJztUCkm0opyjz-yXNc
                sudo docker pull srikanth/nodo-todo-app-test:latest
                sudo docker stop nodetodoapp || true
                sudo docker rm nodetodoapp || true 
                sudo docker run -d --name nodetodoapp srikanth/nodo-todo-app-test:latest
                '''
            }
        }
    }
}
