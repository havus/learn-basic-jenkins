pipeline {
  agent {
    node {
      label 'linux && java11'
    }
  }
  stages {
    stage('Hello') {
      steps {
        echo 'Hello World'
      }
    }
    stage('Hello2') {
      steps {
        echo 'Hello World 1'
      }
    }
  }
  post {
    always {
      echo 'always post'
    }
    success {
      echo 'success post'
    }
    failure {
      echo 'failure post'
    }
    cleanup {
      echo 'cleanup post'
    }
  }
}
