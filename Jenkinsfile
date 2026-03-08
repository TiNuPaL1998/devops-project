pipeline {
    agent any

    environment {
        IMAGE_NAME = "tinupal/devops-project"
        TAG = "latest"
    }

    stages {

        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/TiNuPaL1998/devops-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$TAG .'
            }
        }

        stage('Push Image to DockerHub') {
            steps {
                sh 'docker push $IMAGE_NAME:$TAG'
            }
        }

    }
}