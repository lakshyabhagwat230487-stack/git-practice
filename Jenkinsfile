pipeline {
    agent any

    parameters {
        string(name: 'APP_PORT', defaultValue: '8081', description: 'Port for application')
    
    string(
        name: 'CONTAINER_NAME',
        defaultValue: 'jenkins-demo-container',
        description: 'change in container name'
        )
        string(
            name: 'DEPLOY',
            defaultValue: 'no',
            description: 'Decides whether the container to run'
            )
    }    

    stages {

        stage('Build') {
            steps {
                echo 'building application'
            }
        }
      stage('Environemnt variable test'){
          steps{
               sh 'echo $BUILD_NUMBER'
        sh 'echo $JOB_NAME'
        sh 'echo $WORKSPACE'
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
            when {
                allOf {
                branch 'main'
                expression {
                    params.DEPLOY == 'yes'
                }
                }
            }
            steps {
                sh 'docker stop jenkins-demo-container || true'
                sh 'docker rm jenkins-demo-container || true'
                sh "docker run -d -p ${params.APP_PORT}:80 --name ${params.CONTAINER_NAME} jenkins-demo"
            }
        }
    }
}
