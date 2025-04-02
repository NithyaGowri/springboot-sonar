pipeline {
  agent any
    tools
    {
        maven 'Maven3'
    }
  environment
      {
        scannerHome = tool 'sonar-scan-server';
        registry = "https://hub.docker.com/spring-boot"
        registryCredential = 'docker-jenkins'
        dockerImage = '' 
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
      
     steps {
              withSonarQubeEnv(credentialsId: 'sonar-key', installationName: 'sonar-scan') {
                sh "${scannerHome}/bin/sonar-scanner"
              }
            }
    }
    stage('Dockerize the application')
    {
      
      steps{
        echo "Building Docker image"
        script{
         sh 'docker build -t nithyagkm/spring:$BUILD_NUMBER .'
         echo "Image build successfully..."
        }
      }
    }           
    stage('Docker lOGIN and Push') {
      agent any
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
        echo "Login successful"
      }
    }

  }
}
