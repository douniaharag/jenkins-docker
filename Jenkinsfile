pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('douniaharag')
    }
    stages {
        stage('Build docker image') {
            steps {
                sh 'docker build -t dounia/flask:${BUILD_NUMBER} .'
            }
        }
        stage('Login to DockerHub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push image') {
            steps {
                sh 'docker push dounia/flask:${BUILD_NUMBER}'
            }
        }
    }
}
