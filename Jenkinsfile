pipeline {
  agent none
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
-Dsonar.host.url=http://172.31.86.101:9000/ \\
-Dsonar.projectKey=JPetstore \\
-Dsonar.login=sqp_e37fb7ba3390a02c38dc33140e7eeb3e1cc5a568'''
      }
    }

    stage('Package') {
      steps {
        sh './mvnw package -DskipTests=true'
        archiveArtifacts '**'
      }
    }

    stage('Integration Test') {
      steps {
        node(label: 'test') {
          sh './mvnw verify -P tomcat90'
        }

      }
    }

    stage('Deploy to Staging') {
      steps {
        node(label: 'test') {
          sh './mvnw cargo:run -P tomcat90'
        }

      }
    }

  }
}