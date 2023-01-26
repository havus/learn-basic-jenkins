pipeline {
  agent {
    node {
      label 'linux && java11'
    }
  }
  stages {
    stage('Build') {
      steps {
        echo 'Hello building...'
        sh('./mvnw clean compile test-compile')
        echo 'Finish deploy'
      }
    }
    stage('Test') {
      steps {
        echo 'Hello testing...'
        sh('./mvnw test')
        echo 'Finish test'
      }
    }
    stage('Deploy') {
      steps {
        echo 'Hello deploying...'
        script {
          for (int i = 0; i < 10; i++) {
            echo "Number ${i}"
          }
        }
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
