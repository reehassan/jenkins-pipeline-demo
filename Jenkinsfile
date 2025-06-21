pipeline {
  agent {
    docker {
      image 'python:3.10' // Docker image has no restrictions
    }
  }

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

    stage('Notify') {
      steps {
        echo "✅ Flask CI/CD pipeline complete!"
      }
    }
  }

  post {
    failure {
      echo "❌ Build failed! Check logs."
    }
  }
}
