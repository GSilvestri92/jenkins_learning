pipeline {
    agent {
        docker {
            image 'python:3.13.5-alpine3.22'
            args '--link docker:dind -e DOCKER_HOST=tcp://docker:2375'
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
                sh '''
                    echo -e "FROM alpine\\nRUN echo Hello from Dockerfile" > Dockerfile
                    docker build -t test-image .
                '''
            }
        }
    }

    services {
        docker {
            image: 'docker:dind'
            privileged: true
        }
    }
}