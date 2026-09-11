pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Test') {
            steps {
                sh 'test -f index.html'
                sh 'test -f Dockerfile'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t my-webapp:latest .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker stop my-webapp || true
                    docker rm my-webapp || true
                    docker run -d --name my-webapp -p 8081:80 my-webapp:latest
                '''
            }
        }
    }
}
