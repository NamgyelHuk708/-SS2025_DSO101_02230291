pipeline {
  agent any
  tools {
    nodejs 'NodeJS-20.x'  // Must match the name in Global Tool Configuration
  }
  stages {
    stage('Install') {
      steps {
        sh 'npm install'
      }
    }
    stage('Test') {
      steps {
        sh 'npm test'  // Assumes test script exists in package.json
      }
    }
    stage('Build') {
      steps {
        sh 'npm run build'  // For React/Next.js apps
      }
    }
    stage('Deploy') {
      steps {
        sh 'echo "Deploying to staging..."'
        // Add deployment commands here
      }
    }
  }
}