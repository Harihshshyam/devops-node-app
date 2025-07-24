pipeline {
  agent any

  stages {
    stage('Clone') {
      steps {
        git 'https://github.com/Harihshshyam/devops-node-app.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          docker.build("sagar592/devops-node-app:${env.BUILD_NUMBER}")
        }
      }
    }

    stage('Push Docker Image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
          sh """
            echo "$PASSWORD" | docker login -u "$USERNAME" --password-stdin
            docker push yourdockerhub/devops-node-app:${env.BUILD_NUMBER}
          """
        }
      }
    }
  }
}

