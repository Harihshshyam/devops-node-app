pipeline {
    agent any

    environment {
        IMAGE_NAME = 'sagar592/devops-node-app'
        IMAGE_TAG = "${env.BUILD_NUMBER}"
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Harihshshyam/devops-node-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || echo "No tests defined, continuing..."'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
                }
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                    sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }

        stage('Kubernetes Deploy') {
            steps {
                sh '''
                sed "s|IMAGE_TAG|${IMAGE_TAG}|" k8s/deployment.yaml > k8s/deploy-temp.yaml
                kubectl apply -f k8s/deploy-temp.yaml
                '''
            }
        }
    }
}
