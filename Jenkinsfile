pipeline {
  agent any

  stages {
    stage('Install Python deps') {
      steps {
        sh 'sudo apt-get update && sudo apt-get install -y python3 python3-pip'
      }
    }

    stage('Test') {
      steps {
        sh 'python3 -m unittest discover'
      }
    }
  }
}
