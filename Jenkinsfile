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
        junit '**/target/surefire-reports/TEST-*.xml'
      }
    }

    stage('Static Analysis') {
      steps {
        sh './mvnw sonar:sonar -Dsonar.host.url=http://44.199.241.35:9000/ -Dsonar.projectKey=JPetstore -Dlicense.skip=true'
      }
    }

  }
}