pipeline {
  agent {
    docker {
        image 'node:lts'
        args '-p 3000:3000'
    }
  }
  environment {
    CI = 'true'
  }
  triggers {
    pollSCM('H */4 * * 1-5')
  }
  stages {
    stage('Build') {
      steps {
        echo 'Building ...'
        echo 'Installing dependencies'
        sh 'npm install'
      }
    }
    stage('Run Unit Tests') {
      steps {
        echo 'Running unit tests'
        sh 'npm run test:unit'
      }
    }
    stage('Deliver') {
      steps {
        echo ''
        sh 'set -x'
        sh 'npm start &'
        sh 'sleep 1'
        echo '$! > .pidfile'
        sh 'set +x'
      }
    }
  }
}
