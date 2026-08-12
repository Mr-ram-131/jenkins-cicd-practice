pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Starting build...'
                bat '"C:\\Users\\pradh\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" --version'
                bat '"C:\\Users\\pradh\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" -m pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                bat '"C:\\Users\\pradh\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" -m pytest'
            }
        }

        stage('Deploy') {
            steps {
                withCredentials([file(credentialsId: 'ec2-key-file', variable: 'SSH_KEY')]) {
                    bat '''
                        ssh -i "%SSH_KEY%" -o StrictHostKeyChecking=no ubuntu@3.110.114.110 "echo Jenkins successfully connected to EC2"
                    '''
                }
            }
        }
    }
}
