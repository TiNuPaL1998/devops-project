pipeline {
    agent any

    stages {

        stage('Clone') {
    steps {
        git branch: 'main', url: 'https://github.com/TiNuPaL1998/devops-project.git'
    }
}

        stage('Build') {
            steps {
                echo "Building project..."
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
            }
        }

    }
}