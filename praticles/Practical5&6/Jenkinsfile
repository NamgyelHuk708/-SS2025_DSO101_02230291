pipeline {
  agent any
  tools {
    nodejs 'NodeJS 24.0.2'
  }
  environment {
    CI = 'true'
    DOCKER_IMAGE = "namgyelhuk708/nodejs-app"
    DOCKER_CREDENTIALS_ID = "dockerhub-creds"
  }
  stages {
    stage('Install') {
      steps {
        sh 'npm install'
      }
    }
    stage('Build') {
      steps {
        sh 'npm ci'
      }
    }
    stage('Test') {
      steps {
        sh 'npm test'
      }
      post {
        always {
          junit 'junit.xml'
        }
      }
    }
    stage('Docker Build') {
      steps {
        script {
          dockerImage = docker.build("${DOCKER_IMAGE}:${BUILD_NUMBER}")
        }
      }
    }
    stage('Docker Push') {
      steps {
        script {
          docker.withRegistry('', DOCKER_CREDENTIALS_ID) {
            dockerImage.push()
            dockerImage.push('latest')
          }
        }
      }
    }
    stage('Deploy') {
      steps {
        script {
          if (env.BRANCH_NAME == 'main') {
            sh 'echo "Deploying to production..."'
            // Add your production deployment commands here
          } else {
            sh 'echo "Deploying to staging..."'
            // Add your staging deployment commands here
          }
        }
      }
    }
  }
}