pipeline {
  agent any
  environment {
    NEXUS_VERSION = "nexus3"
    NEXUS_PROTOCOL = "http"
    NEXUS_URL = "localhost:8081"
    NEXUS_REPOSITORY = "JPetstore"
    NEXUS_CREDENTIAL_ID = "nexus-user-credentials"
  }
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
-Dsonar.host.url=http://localhost:9000/ \\
-Dsonar.projectKey=JPetstore \\
-Dsonar.login=sqp_e37fb7ba3390a02c38dc33140e7eeb3e1cc5a568'''
      }
    }

    stage('Package') {
      steps {
        sh './mvnw package -DskipTests=true'
      }
    }

    stage('Deploy to Nexus') {
      steps {
        nexusArtifactUploader(
        nexusVersion: 'nexus3',
        protocol: 'http',
        nexusUrl: 'localhost:8081',
        groupId: 'tsdevopsacp',
        version: version,
        repository: 'JPetstore',
        credentialsId: 'nexus-user-credentials',
        artifacts: [
            [artifactId: projectName,
             classifier: '',
             file: 'jpetstore-' + version + '.war',
             type: 'war']
        ]
     )
      }
    }
  }
}
