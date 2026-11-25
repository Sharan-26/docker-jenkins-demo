pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Starting Docker integration'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t jenkins-nginx:v1 .'
            }
        }

        stage('Docker Images') {
            steps {
                sh 'docker images'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                    docker rm -f jenkins-nginx || true

                    docker run -d \
                    --name jenkins-nginx \
                    -p 8080:80 \
                    jenkins-nginx:v1
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'docker ps'
                sh 'curl -I http://localhost:8080'
            }
        }
    }
}
