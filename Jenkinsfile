pipeline {
  agent any

  environment {
    IMAGE_NAME = "nour12378/student-management"
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build JAR') {
      steps {
        sh "mvn -B clean package -DskipTests"
      }
    }

    stage('Build Docker Image') {
      steps {
        sh "docker build -t ${IMAGE_NAME}:latest ."
      }
    }

    stage('Docker Login') {
      steps {
        withCredentials([usernamePassword(credentialsId: '0e98e89a-093e-4271-95c5-a704b2337aec', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
          sh "echo \$PASS | docker login -u \$USER --password-stdin"
        }
      }
    }

    stage('Push Image') {
      steps {
        sh "docker push ${IMAGE_NAME}:latest"
      }
    }
  }
}
