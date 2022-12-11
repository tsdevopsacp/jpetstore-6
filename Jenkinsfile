pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'first jenkins pipeline'
        sh './mvnw clean compile'
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
        sh '''./mvnw sonar:sonar \\
-Dsonar.host.url=http://44.199.241.35:9000/ \\
-Dsonar.projectKey=JPetstore \\
-Dsonar.login=sqp_4505d30134524c4bce45ca1528f2356257076e44'''
      }
    }

    stage('Package') {
      steps {
        sh './mvnw package'
      }
    }

    stage('Deploy to Nexus') {
      steps {
        sh './mvnw deploy'
      }
    }

  }
}