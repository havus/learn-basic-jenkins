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
          def data = [
            'firstName': 'John',
            'lastName': 'Doe'
          ]

          for (int i = 0; i < 10; i++) {
            echo "Number ${i}"
          }

          writeJSON(file: 'data.json', json: data)
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
