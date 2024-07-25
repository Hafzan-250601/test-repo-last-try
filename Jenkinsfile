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
        apt-get update && apt-get upgrade -y
        apt-get install python3 python3-pip python3-venv -y
        python3 -m venv .venv
        . .venv/bin/activate
        pip install pytest selenium
        docker compose up -d
        sleep 20
        python3 test_devopstest.py
        '''
      }
    }
  }
}