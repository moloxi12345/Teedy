pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('Doc') {
            steps {
                sh 'mvn javadoc:javadoc'
            }
        }
    stage('pmd') {
      steps {
        sh 'mvn pmd:pmd'
      }
    }
   stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
  }
post {
  always {
    archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
    archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
    archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
    archiveArtifacts artifacts: '**/target/surefire-reports/*.xml', fingerprint: true
    archiveArtifacts artifacts: '**/target/site/apidocs/**', fingerprint: true
    archiveArtifacts artifacts: '**/target/surefire-reports/TEST-*.xml', fingerprint: true
  }
}
}