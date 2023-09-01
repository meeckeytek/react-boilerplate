pipeline {
    agent any
    stages {
        stage('Building Docker Image') {
            steps {
                script {
                    echo 'Building Docker Image'
                    sh 'docker build -t meeckey/react-app:1.0 .'
                }
            }
        }

        stage('Pushing to Docker Hub') {
            steps {
                script {
                    echo 'Pushing the Image to Docker Hub'
                    sh 'docker push meeckey/react-app:1.0'
                }
            }
        }

        stage('Deploying to Remote Server') {
            steps {
                script {
                    echo 'Deploying the application to Remote server'
                    def dockerCmd = 'docker run -p 3000:3000 -d meeckey/react-app:1.0'
               sshagent(['vm-server-key']) {
                    sh "ssh -o StrictHostKeyChecking=no <remote-server-username>@<remote-server-IP> ${dockerCmd}"
                   }
                }
            }
        }
    }
}