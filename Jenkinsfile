pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhub'
        DOCKERHUB_NAMESPACE = 'arehmanse'
    }

    stages {
        stage('i211133 Build Auth Image') {
            steps {
                script {
                    echo "Building Auth Image"
                    def authImage = docker.build("${DOCKERHUB_NAMESPACE}/authbackend", './Auth')
                    authImage.push()
                }
            }
        }
        stage('i211133 Build Classrooms Image') {
            steps {
                script {
                    echo "Building Classrooms Image"
                    def classroomsImage = docker.build("${DOCKERHUB_NAMESPACE}/classroomsbackend", './Classrooms')
                    classroomsImage.push()
                }
            }
        }
        stage('i211133 Build Client Image') {
            steps {
                script {
                    echo "Building Client Image"
                    def clientImage = docker.build("${DOCKERHUB_NAMESPACE}/client", './client')
                    clientImage.push()
                }
            }
        }
        stage('i211133 Build Event Bus Image') {
            steps {
                script {
                    echo "Building Event Bus Image"
                    def eventBusImage = docker.build("${DOCKERHUB_NAMESPACE}/eventbus", './event-bus')
                    eventBusImage.push()
                }
            }
        }
        stage('i211133 Push Images to Docker Hub') {
            steps {
                script {
                    echo "Pushing Images to Docker Hub"
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
            echo "Cleaning workspace"
            cleanWs()
        }
    }
}
