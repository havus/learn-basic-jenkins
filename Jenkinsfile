pipeline {
  agent {
    node {
      label 'linux && java11'
    }
  }

  environment {
    AUTHOR  = 'John Doe'
    EMAIL   = 'johndoe@mail.com'
    WEB     = 'example.com'
  }

  options {
    disableConcurrentBuilds() // build jalan satu per satu
    timeout(time: 30, unit: 'MINUTES')
  }

  parameters {
    string(name: 'NAME', defaultValue: 'Guest', description: 'Your Name')
    text(name: 'DESCRIPTION', defaultValue: 'Guest', description: 'Tell me about you')
    booleanParam(name: 'DEPLOY', defaultValue: false, description: 'Need to Deploy?')
    choice(name: 'SOCIAL_MEDIA', choices: ['Instagram', 'Facebook', 'Twitter'], description: 'Which social media?')
    password(name: 'SECRET', defaultValue: '', description: 'Encrypted key')
  }

  triggers {
    cron('0 0 * * *')
    // pollSCM('0 0 * * *')
    // upstream(upstreamProjects: 'job1,job2', threshold: hudson.model.Result.SUCCESS)
  }

  stages {
    stage('Print Parameters') {
      steps {
        echo "NAME: ${params.NAME}"
        echo "DESCRIPTION: ${params.DESCRIPTION}"
        echo "DEPLOY: ${params.DEPLOY}"
        echo "SOCIAL_MEDIA: ${params.SOCIAL_MEDIA}"
        echo "SECRET: ${params.SECRET}"
      }
    }

    stage('Build') {
      steps {
        echo 'Hello building...'
        echo "Start Job: ${env.JOB_NAME}"
        echo "Start Job: ${env.BUILD_NUMBER}"
        echo "Start Job: ${env.BRANCH_NAME}" // will null except new job with multi branch pipelinne
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
      input {
        // id 'default is stage name'
        message 'can we deploy?'
        ok 'yes of course!'
        submitter 'havus'
        parameters {
          choice(name: 'TARGET_ENV', choices: ['Staging', 'Sandbox', 'Production'], description: 'Which environment?')
        }
      }
      // agent {
      //   node {
      //     label 'linux && java11'
      //   }
      // }
      steps {
        echo 'Hello deploying...'
        echo "Environment ${TARGET_ENV}"

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
