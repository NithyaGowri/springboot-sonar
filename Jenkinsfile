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
    stage('Dockerize the application')
    {
      environment
      {
            DOCKER_IMAGE = 'trail-app'
            IMAGE_TAG = 'latest'
            DOCKER_CREDENTIALS = 'docker-jenkins'  // Jenkins credentials ID for Docker Hub or your registry
            USERNAME= 'nithyagkm'
      }
      steps{
        echo "Building Docker image"
        script{
          sh 'docker build -t ${DOCKER_IMAGE}:${IMAGE_TAG} .'
        }
      }
    }           
    stage('Docker Push') {
      agent any
      steps {
        withCredentials([usernamePassword(credentialsId: 'docker-jenkins', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push'
        }
      }
    }

  }
}
