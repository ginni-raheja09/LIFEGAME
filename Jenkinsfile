pipeline {  
    agent any  
  
    environment {  
        MAVEN_HOME = tool 'Maven' // Name of the Maven tool configured in Jenkins  
        JAVA_HOME = tool 'JDK' // Name of the JDK tool configured in Jenkins  
        PATH = "${env.MAVEN_HOME}/bin:${env.JAVA_HOME}/bin:${env.PATH}"  
    }  
  
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
        stage('Test') {  
            steps {  
                // Run the tests  
                sh 'mvn test'  
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
