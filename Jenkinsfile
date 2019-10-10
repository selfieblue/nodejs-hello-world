pipeline {
  agent any
  environment {
      scannerHome = tool 'sonarqube-scanner'
  }
  stages {
    stage("build & SonarQube analysis") {
      agent any
      steps {
          withSonarQubeEnv('sonarqube-server') {
              sh "${scannerHome}/bin/sonar-scanner -Dsonar.language=js -Dsonar.login=ba66e73d2725b51d34f0c8cfcabe6ebb9a04495c -Dsonar.projectKey=demo -Dsonar.projectName=demo -Dsonar.projectVersion=1.0.0"
          }
      }
    }
    stage("Quality Gate") {
      steps {
        timeout(time: 10, unit: 'MINUTES') {
          waitForQualityGate abortPipeline: true
        }
      }
    }
  }
}