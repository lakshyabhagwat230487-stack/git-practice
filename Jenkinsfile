pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'building application'
            }
        }

        stage('Test') {
            steps {
                sh 'echo running test'
                sh 'test 5 -eq 5'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t jenkins-demo .'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker stop jenkins-demo-container || true'
                sh 'docker rm jenkins-demo-container || true'
                sh 'docker run -d -p 8081:80 --name jenkins-demo-container jenkins-demo'
            }
        }
    }
}
