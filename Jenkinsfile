pipeline {
   agent any


   environment {
       DOCKER_REPO = 'arehmanse'
   }


   stages {
     


       stage('i211133 Build Docker Images') {
           parallel {
               stage('i211133 Build Auth Image') {
                   steps {
                       script {
                           def app = docker.build("${DOCKER_REPO}/auth", './auth')
                       }
                   }
               }


               stage('i211133 Build Classrooms Image') {
                   steps {
                       script {
                           def app = docker.build("${DOCKER_REPO}/classroom", './classroom')
                       }
                   }
               }


               stage('i211133 Build Client Image') {
                   steps {
                       script {
                           def app = docker.build("${DOCKER_REPO}/client", './client')
                       }
                   }
               }


               stage('i211133 Build Event-Bus Image') {
                   steps {
                       script {
                           def app = docker.build("${DOCKER_REPO}/event", './event')
                       }
                   }
               }


               stage('i211133 Build Post Image') {
                   steps {
                       script {
                           def app = docker.build("${DOCKER_REPO}/post", './post')
                       }
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




