pipeline {
    agent {
        docker {
            image 'python:3.13.5-alpine3.22'
            args '--privileged -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages {
        stage('Check Python') {
            steps {
                sh 'python --version'
            }
        }

        stage('Check Docker') {
            steps {
                sh 'docker version'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    writeFile file: 'Dockerfile', text: '''
                        FROM alpine
                        RUN echo "Hello from Dockerfile"
                    '''
                    sh 'docker build -t test-image .'
                }
            }
        }
    }
}