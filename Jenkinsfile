pipeline {
    agent any

    environment {
      DOCKERHUB_CREDENTIALS='docker_credential_c2'
      IMAGE_NAME = 'rohi367/new_docker_image'
      }

    stages {

        stage('Build java application') {
            steps {
                bat 'javac Helloworld.java'
            }
        }
      stage('Run java program') {
            steps {
                bat 'java Helloworld'
            }
        }

      stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:latest .'
            }
        }
   


        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker_credential_c2',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    bat 'echo %PASS%| docker login -u %USER% --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push %IMAGE_NAME%:latest'
            }
        }
    }
}
