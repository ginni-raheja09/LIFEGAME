pipeline {  
    agent none // No global agent; specify agents at the stage level  
    environment {  
        KUBERNETES_SKIP_TLS_VERIFY = 'true'
        KUBECONFIG = credentials('config') // Reference the kubeconfig credential ID  
    }  
    stages {  
        stage('Checkout') {  
            agent {  
                kubernetes {  
                    yaml """  
                    apiVersion: v1  
                    kind: Pod  
                    spec:  
                      containers:  
                      - name: maven  
                        image: maven:3.6.3-jdk-8  
                        command:  
                        - cat  
                        tty: true  
                        volumeMounts:  
                        - name: maven-repo  
                          mountPath: /root/.m2  
                      volumes:  
                      - name: maven-repo  
                        persistentVolumeClaim:  
                          claimName: maven-repo-pvc  
                    """  
                    defaultContainer 'maven'  
                }  
            }  
            steps {  
                // Checkout the source code from the repository  
                checkout scm  
                // Stash the checked out source code to reuse in other stages if needed  
                stash name: 'source', includes: '**/*'  
            }  
        }  
    }  
  
    post {  
        success {  
            echo 'Checkout completed successfully!'  
        }  
        failure {  
            echo 'Checkout stage failed.'  
        }  
    }  
}  
