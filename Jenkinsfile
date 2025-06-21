pipeline {
  agent {
    docker {
      image 'python:3.10'
    }
  }

  stages {
    stage('Test') {
      steps {
        sh 'python -m unittest discover'
      }
    }
  }
}
