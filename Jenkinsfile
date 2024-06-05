pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhub'
    }

    stages {
        stage('Build Auth Image') {
            steps {
                script {
                    echo "Building Auth Image"
                    docker.build('authbackend', './Auth')
                }
            }
        }
        stage('Build Classrooms Image') {
            steps {
                script {
                    echo "Building Classrooms Image"
                    docker.build('classroomsbackend', './Classrooms')
                }
            }
        }
        stage('Build Client Image') {
            steps {
                script {
                    echo "Building Client Image"
                    docker.build('client', './client')
                }
            }
        }
        stage('Build Event Bus Image') {
            steps {
                script {
                    echo "Building Event Bus Image"
                    docker.build('eventbus', './event-bus')
                }
            }
        }
        stage('Push Images to Docker Hub') {
            steps {
                script {
                    echo "Pushing Images to Docker Hub"
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                        docker.image('authbackend').push('latest')
                        docker.image('classroomsbackend').push('latest')
                        docker.image('client').push('latest')
                        docker.image('eventbus').push('latest')
                    }
                }
            }
        }
    }

    post {
        always {
            echo "Cleaning workspace"
            cleanWs()
        }
    }
}
