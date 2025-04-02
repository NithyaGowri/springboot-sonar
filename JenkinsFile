pipeline {
  agent any
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
        SONAR_URL = "http://192.168.56.1:9000"
      }
     steps {
              withSonarQubeEnv(credentialsId: 'sonar-key', installationName: 'sonar-scan') {
                sh "${SONAR_URL}/bin/sonar-scanner"
              }
            }
    }
  }
}
