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
        sh './mvnw package -DskipTests=true'
      }
    }

    stage('Deploy to Nexus') {
      steps {
        nexusArtifactUploader(nexusVersion: '3.4', protocol: 'http', nexusUrl: '44.203.142.100:8081', groupId: 'tsdevopsacp', version: '1.0.0', repository: 'JPetsore', credentialsId: 'admin')
      }
    }

  }
}