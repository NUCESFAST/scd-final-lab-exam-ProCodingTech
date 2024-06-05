pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhub'
        DOCKERHUB_NAMESPACE = 'arehmanse'
    }

    stages {
        stage('Build Auth Image') {
            steps {
                script {
                    docker.build("${DOCKERHUB_NAMESPACE}/authbackend", './Auth')
                }
            }
        }
        stage('Build Classrooms Image') {
            steps {
                script {
                    docker.build("${DOCKERHUB_NAMESPACE}/classroomsbackend", './Classrooms')
                }
            }
        }
        stage('Build Client Image') {
            steps {
                script {
                    docker.build("${DOCKERHUB_NAMESPACE}/client", './client')
                }
            }
        }
        stage('Build Event Bus Image') {
            steps {
                script {
                    docker.build("${DOCKERHUB_NAMESPACE}/eventbus", './event-bus')
                }
            }
        }
        stage('Push Images to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                        docker.image("${DOCKERHUB_NAMESPACE}/authbackend").push()
                        docker.image("${DOCKERHUB_NAMESPACE}/classroomsbackend").push()
                        docker.image("${DOCKERHUB_NAMESPACE}/client").push()
                        docker.image("${DOCKERHUB_NAMESPACE}/eventbus").push()
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
