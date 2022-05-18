pipeline {
  agent any 
  environment {
    DB_CREDS=credentials('sqlservercreds')
  }
  stages {
    stage('Verify version') {
      steps {
        sh 'docker run --rm flyway/flyway:8.5.1 version'
      }
    }
    stage('migrate') {
      steps {
        sh 'docker run --rm -v $WORKSPACE/sql:/flyway/sql -v $WORKSPACE/conf:/flyway/conf flyway/flyway:8.5.1 migrate'
      }
    }
    stage('validate') {
      steps {
        sh 'docker run --rm -v $WORKSPACE/sql:/flyway/sql -v $WORKSPACE/conf:/flyway/conf flyway/flyway:8.5.1 validate'
      }
    }
    stage('info') {
      steps {
        sh 'docker run --rm -v $WORKSPACE/sql:/flyway/sql -v $WORKSPACE/conf:/flyway/conf flyway/flyway:8.5.1 info'
      }
    }
  }
}
