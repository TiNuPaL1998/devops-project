pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "tinupal/devops-project"
        DOCKER_TAG = "latest"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/TiNuPaL1998/devops-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:$DOCKER_TAG .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    '''
                }
            }
        }

        stage('Push Image to DockerHub') {
            steps {
                sh 'docker push $DOCKER_IMAGE:$DOCKER_TAG'
            }
        }

        stage('Deploy to EC2 using Ansible') {
            steps {
                sh 'ansible-playbook deploy.yml -i inventory'
            }
        }

    }

    post {
        success {
            echo "Deployment Successful!"
        }

        failure {
            echo "Pipeline Failed!"
        }
    }
}