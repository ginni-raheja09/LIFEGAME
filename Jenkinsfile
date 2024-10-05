pipeline {  
    agent none // No global agent; specify agents at the stage level  
      
    stages {  
        stage('Build') {  
            agent {  
                kubernetes {  
                    cloud 'kubernetes' // Name of the Kubernetes cloud configuration  
                    label 'jenkins-maven-agent' // Label to match the AKS node labels  
                    defaultContainer 'maven'  
                    yaml """  
                    apiVersion: v1  
                    kind: Pod  
                    metadata:  
                      labels:  
                        jenkins-agent: maven  
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
                      nodeSelector:  
                        kubernetes.io/hostname: <your-aks-node-label>  
                    """  
                }  
            }  
            steps {  
                // Build your Maven project  
                container('maven') {  
                    sh 'mvn clean package'  
                }  
            }  
        }  
    }  
  
    post {  
        success {  
            echo 'Build completed successfully!'  
        }  
        failure {  
            echo 'Build failed.'  
        }  
    }  
}  
