pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/Manish-kz/jen-cd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t project2-app .'
            }
        }

        stage('Test Application') {
            steps {
                bat '''
                docker run -d -p 5000:5000 --name test_app project2-app
                timeout /t 5
                docker stop test_app
                docker rm test_app
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                bat '''
                docker rm -f project2-container || exit 0
                docker run -d -p 5000:5000 --name project2-container project2-app
                '''
            }
        }
    }
}