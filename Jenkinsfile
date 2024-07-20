pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dounia-dockerhub')
    }
    stages {
        stage('Build docker image') {
            steps {
                sh 'docker build -t douniaharag/flaskapp:${BUILD_NUMBER} .'
            }
        }
        stage('Login to DockerHub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push image') {
            steps {
                sh 'docker push douniaharag/flaskapp:${BUILD_NUMBER}'
            }
        }
    }
}
