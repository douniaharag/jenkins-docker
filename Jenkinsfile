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
        stage('Scan Docker Image') {
            steps {
                script {
                    def trivyOutput = sh(script: "trivy image douniaharag/flaskapp:${BUILD_NUMBER}", returnStdout: true).trim()
                    println trivyOutput
                    if (trivyOutput.contains("Total: 0")) {
                        echo "No vulnerabilities found in the Docker image."
                    } else {
                        echo "Vulnerabilities found in the Docker image."
                        // Uncomment the next line if you want to fail the build when vulnerabilities are found
                        // error "Vulnerabilities found in the Docker image."
                    }
                }
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
