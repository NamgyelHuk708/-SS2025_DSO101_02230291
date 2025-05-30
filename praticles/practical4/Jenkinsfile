pipeline {
  agent any
  tools {
    nodejs 'NodeJS 24.0.2' 
  }
  
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    
    stage('Install') {
      steps {
        sh 'npm install'
      }
    }
    
    stage('Test') {
      steps {
        sh 'npm run test:ci'
      }
      post {
        always {
          junit 'junit.xml'
          archiveArtifacts artifacts: 'junit.xml', fingerprint: true
        }
      }
    }
    
    stage('Build') {
      steps {
        sh 'npm run build'
      }
    }
    
    stage('Deploy') {
      steps {
        sh 'echo "Deploying to staging..."'
      }
    }
  }
  
  post {
    always {
      archiveArtifacts artifacts: 'coverage/**/*', fingerprint: true
    }
  }
}