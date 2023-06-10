pipeline {
  agent any
  
  stages {
    stage('Checkout') {
      steps {
        // Checkout your code from version control system (e.g., Git)
        git 'https://github.com/your-repo.git'
      }
    }
    
    stage('Unit Test') {
      steps {
        // Run unit tests using your preferred testing framework (e.g., JUnit)
        sh 'mvn test' // Assuming you're using Maven for Java project
      }
    }
    
    stage('Integration Test') {
      steps {
        // Run integration tests using your preferred testing framework (e.g., Selenium, Cucumber)
        // Set up test environment if necessary
        sh 'mvn integration-test'
      }
    }
    
    stage('SonarQube Analysis') {
      steps {
        // Run SonarQube analysis on your code
        withSonarQubeEnv('SonarQube') {
          sh 'mvn sonar:sonar'
        }
      }
    }
    
    stage('Build Docker Image') {
      steps {
        // Build a Docker image for your application
        sh 'docker build -t your-image:latest .'
      }
    }
    
    stage('Push Docker Image') {
      steps {
        // Push the Docker image to a Docker registry (e.g., Docker Hub)
        withDockerRegistry([credentialsId: 'docker-credentials', url: 'https://registry.example.com']) {
          sh 'docker push your-image:latest'
        }
      }
    }
    
    stage('Deploy to Kubernetes') {
      steps {
        // Deploy your application to Kubernetes
        withKubeConfig([credentialsId: 'kubernetes-credentials', kubeconfigId: 'kubeconfig']) {
          sh 'kubectl apply -f your-deployment.yaml'
        }
      }
    }
  }
}
