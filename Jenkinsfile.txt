pipeline {
    agent any  // Runs on any available Jenkins agent
    
    environment {
        DEPLOY_PATH = "C:\\deploy\\"  // Change this for Windows deployments
    }

    stages {
        stage('Pull Code') {
            steps {
                git 'https://github.com/your-username/jenkins-demo.git'  // Replace with your repo
            }
        }
        
        stage('Build') {
            steps {
                bat 'mvn clean package'  // Windows command to build using Maven
            }
        }
        
        stage('Test') {
            steps {
                bat 'mvn test'  // Run unit tests
            }
        }
        
        stage('Deploy') {
            steps {
                bat "copy target\\sample-app.jar ${DEPLOY_PATH}"  // Copy JAR file to deployment directory
            }
        }
    }
    
    post {
        success {
            echo '🎉 Deployment Successful!'
        }
        failure {
            echo '❌ Deployment Failed!'
        }
    }
}
