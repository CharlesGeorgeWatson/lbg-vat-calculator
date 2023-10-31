pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        //  Get some code from a GitHub repo
        git branch: 'main', url: 'https://github.com/CharlesGeorgeWatson/lbg-vat-calculator'
      }
    }
    stage('SonarQube Analysis') {
      environment {
        scannerHome = tool 'sonarqube'
      }
      steps {
        withSonarQubeEnv('sonar-qube-1') {
          sh "${scannerHome}/bin/sonar-scanner"
        }
          timeout(time: 10, unit: 'MINUTES'){
        waitForQualityGate abortPipeline: true
      }
    }
    
  }
}
}
