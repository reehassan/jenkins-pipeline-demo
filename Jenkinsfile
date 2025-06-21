pipeline {
  agent any

  environment {
    IMAGE_NAME = 'flask-ci-cd-demo'
    TAG = 'latest'
  }

  stages {

    stage('Install Deps') {
      steps {
        sh 'pip install -r requirements.txt'
      }
    }

    stage('Run Tests') {
      steps {
        sh 'python -m unittest discover'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh "docker build -t $IMAGE_NAME:$TAG ."
      }
    }

    stage('Deploy Container') {
      steps {
        sh '''
          docker rm -f flask_app || true
          docker run -d --name flask_app -p 5000:5000 $IMAGE_NAME:$TAG
        '''
      }
    }

    // Optional
    stage('Notify') {
      steps {
        echo "Build & Deploy complete!"
        // For Slack: Use slackSend plugin (optional)
      }
    }
  }

  post {
    failure {
      echo "❌ Build failed! Check logs."
      // Optional: Send failure alert
    }
  }
}
