pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Starting build...'
                bat 'python --version'
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                bat 'pytest'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }
    }
}
