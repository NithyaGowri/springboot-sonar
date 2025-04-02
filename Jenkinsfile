pipeline {
  agent any
    tools
    {
        maven 'Maven3'
    }
  stages {
    stage('Checkout') {
      steps {
        sh 'echo passed'
        //git branch: 'main', url: 'https://github.com/iam-veeramalla/Jenkins-Zero-To-Hero.git'
      }
    }
    stage('Build and Test') {
      steps {
        sh 'ls -ltr'
        // build the project and create a JAR file
        sh 'mvn clean package'      
}
    }
    stage('Static Code Analysis') {
      environment {
        scannerHome = tool 'sonar-scan-server';
      }
     steps {
              withSonarQubeEnv(credentialsId: 'sonar-key', installationName: 'sonar-scan') {
                sh "${scannerHome}/bin/sonar-scanner"
              }
            }
    }
  }
}
