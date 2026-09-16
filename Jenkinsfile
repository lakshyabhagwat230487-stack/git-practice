pipeline {
    agent any

    parameters {
        string(name: 'APP_PORT', defaultValue: '8081', description: 'Port for application')
    
    string(
        name: 'CONTAINER_NAME',
        defaultValue: 'jenkins-demo-container',
        description: 'change in container name'
        )
    }    

    stages {

        stage('Build') {
            steps {
                echo 'building application'
            }
        }

        stage('Test') {
            steps {
                sh 'test -f index.html'
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
                sh "docker run -d -p ${params.APP_PORT}:80 --name ${params.CONTAINER_NAME} jenkins-demo"
            }
        }
    }
}
