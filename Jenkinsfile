pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker compose up -d'
        sh '''
        pip install virtualenv
        python3 -m venv venv
        . venv/bin/activate
        pip install pytest selenium
        docker compose up -d
        sleep 20
        python3 test_devopstest.py
        '''
      }
    }
  }
}