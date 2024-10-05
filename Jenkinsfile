pipeline {  
    agent any 
    stages {  
        stage('Checkout') {  
            steps {  
                // Checkout the source code from the repository  
                checkout scm  
            }  
        }  
        stage('Build') {  
            steps {  
                // Build the Java application using Maven  
                sh 'mvn clean compile'  
            }  
        }  
        stage('Package') {  
            steps {  
                // Package the application  
                sh 'mvn package'  
            }  
        }  
        stage('Deploy') {  
            steps {  
                // Deploy the application (this can be customized as per your deployment strategy)  
                echo 'Deploying the application...'  
                // Example: sh 'scp target/gameoflife.jar user@server:/path/to/deploy'  
            }  
        }  
    }  
  
    post {  
        always {  
            // Clean up workspace  
            cleanWs()  
        }  
        success {  
            // Notify success (e.g., email, Slack, etc.)  
            echo 'Build and deployment successful!'  
        }  
        failure {  
            // Notify failure  
            echo 'Build or deployment failed.'  
        }  
    }  
}  
