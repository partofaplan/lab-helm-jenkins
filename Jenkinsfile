pipeline {
    agent any

    environment {
        AWS_ACCOUNT_ID = '047758017848'
        AWS_REGION = 'us-east-2'
        ECR_REPO = 'weathervane'
        EKS_NAMESPACE = 'weathervane'
    }

    stages {
        stage('Clone and Build') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/partofaplan/weathervane-py.git']]])

                script {
                    def dockerImage = docker.build("${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${ECR_REPO}:latest", "-f Dockerfile .")
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials') {
                        dockerImage.push()
                    }
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                script {
                    sh "helm upgrade --install myapp -n ${EKS_NAMESPACE} -f values.yaml weathervane-py-charts/weathervane-py"
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
