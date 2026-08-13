pipeline {
    agent any

    environment {
        EC2_HOST = '65.0.177.86'
        APP_NAME = 'cicd-flask-app'
        APP_PORT = '5000'
    }

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

                withCredentials([
                    file(credentialsId: 'newec2-key-file', variable: 'SSH_KEY')
                ]) {

                    bat '''
                        icacls "%SSH_KEY%" /inheritance:r
                        icacls "%SSH_KEY%" /grant:r "SYSTEM:F"
                        icacls "%SSH_KEY%" /grant:r "Administrators:F"

                        ssh -i "%SSH_KEY%" -o StrictHostKeyChecking=no ubuntu@%EC2_HOST% "echo Connected to EC2"
                    '''
                }
            }
        }
    }
}
