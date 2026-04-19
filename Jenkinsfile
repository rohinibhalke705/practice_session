pipeline {
    agent any

    environment {
      DOCKERHUB_CREDENTIALS='Docker_hub_image'
      IMAGE_NAME = 'rohi367/new_docker_image_1'
      }

    stages {

        stage('Build java application') {
            steps {
                bat 'javac Main.java'
            }
        }
      stage('Run java program') {
            steps {
                bat 'java Main'
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
                    credentialsId: 'Docker_hub_image',
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
