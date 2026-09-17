pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building application'
                sh 'ls -la'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application'
                sh 'test -f index.html'
                sh 'test -f Dockerfile'
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Building Docker image'
                sh 'sudo docker build -t cicd-demo .'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application'

                sh '''
                sudo docker stop cicd-demo-container || true
                sudo docker rm cicd-demo-container || true

                sudo docker run -d \
                --name cicd-demo-container \
                -p 80:80 \
                cicd-demo
                '''
            }
        }

        stage('Docker Details') {
            steps {
                sh 'sudo docker images'
                sh 'sudo docker ps'
            }
        }
    }
}
