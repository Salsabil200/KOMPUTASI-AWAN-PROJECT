pipeline {
  agent any
  environment {
    IMAGE_NAME = 'sabrina200/komputasi-awan-project'
    REGISTRY   = 'https://index.docker.io/v1/'
    REGISTRY_CREDENTIALS = 'dockerhub-credentials'
  }
  stages {
    stage('Checkout') {
      steps { checkout scm }
    }
    stage('Build Docker Image') {
      steps {
        script {
          echo '🚧 Build Docker image'
          docker.build("${IMAGE_NAME}:${env.BUILD_NUMBER}")
        }
      }
    }
    stage('Push Docker Image') {
      steps {
        script {
          echo '📤 Push to Docker Hub'
          docker.withRegistry(REGISTRY, REGISTRY_CREDENTIALS) {
            def tag = "${IMAGE_NAME}:${env.BUILD_NUMBER}"
            docker.image(tag).push()
            docker.image(tag).push('latest')
          }
        }
      }
    }
  }
  post { always { echo "✅ Selesai – tag ${env.BUILD_NUMBER}" } }
}
