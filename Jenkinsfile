pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/partofaplan/weathervane-py.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("weathervane:${env.BUILD_NUMBER}")
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'kubectl apply -f kubernetes-manifests.yaml'
                }
            }
        }
    }
}
