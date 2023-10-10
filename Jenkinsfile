pipeline {
  agent any
  stages {
    stage('error') {
      steps {
        echo 'First commit'
        sh './mvnw clean compile'
      }
    }

  }
}