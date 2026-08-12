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
        withCredentials([file(credentialsId: 'newec2-key-file', variable: 'SSH_KEY')]) {
            bat '''
                icacls "%SSH_KEY%" /inheritance:r
                icacls "%SSH_KEY%" /grant:r "SYSTEM:F"
                icacls "%SSH_KEY%" /grant:r "Administrators:F"

                ssh -i "%SSH_KEY%" -o StrictHostKeyChecking=no ubuntu@13.235.67.74 "cd ~/git_practice && git pull origin master && docker build -t cicd-flask-app:latest . && docker stop cicd-flask-app || true && docker run -d --name cicd-flask-app -p 5000:5000 cicd-flask-app:latest && sleep 5 && curl -f http://localhost:5000/health"
            '''
        }
    }
}
    }
}
