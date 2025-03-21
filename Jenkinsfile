pipeline {
    agent any
    tools {
        maven 'Maven-3.9.9'  // Use the exact name set in Jenkins
    }
    environment {
        DOCKER_CREDENTIALS_ID = 'docker-hub-credentials' // Your Jenkins Docker credentials ID
        IMAGE_NAME = 'ashif321/my-app'
        IMAGE_TAG = 'latest'
    }
    stages {
        stage('Build') {
            steps {
                script {
                    sh 'mvn clean package' // Use Maven to build Java app
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $IMAGE_NAME:$IMAGE_TAG ."
                }
            }
        }
        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: DOCKER_CREDENTIALS_ID, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    sh "docker push $IMAGE_NAME:$IMAGE_TAG"
                }
            }
        }
    }
}
