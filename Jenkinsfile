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
        nexusArtifactUploader(nexusVersion: '3.4', protocol: 'http', nexusUrl: 'localhost:8081', groupId: 'tsdevopsacp', version: '1.0.0', repository: 'JPetsore', credentialsId: 'nexus-user-credentials', artifacts: [
                      [artifactId: projectName,
                      classifier: '',
                      file: 'jpetstore-' + version + '.war',
                      type: 'war']
                    ])
        }
      }

    }
  }