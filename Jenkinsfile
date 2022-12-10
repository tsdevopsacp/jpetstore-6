pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'first jenkins pipeline'
      }
    }

    stage('Unit Test') {
      steps {
        sh './mvnw test'
        junit '/target/surefire-reports/*.xml'
      }
    }

  }
}