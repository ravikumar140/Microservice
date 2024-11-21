pipeline {
    agent any

    stages {
        stage('Deploy To K8s') {
            steps {
                withKubeCredentials(kubectlCredentials: [[
                    caCertificate: '', 
                    clusterName: 'EKS-1', 
                    contextName: '', 
                    credentialsId: 'k8-token', 
                    namespace: 'webapps', 
                    serverUrl: 'https://EC74F1F36DBFD35119E0E221FA503E41.gr7.ap-south-1.eks.amazonaws.com'
                ]]) {
                    sh '''
                        echo "Applying Kubernetes resources..."
                        ls -l  # Debug step to verify the workspace contents
                        kubectl apply -f deployment-service.yml  # Corrected file name
                    '''
                }
            }
        }
        
        stage('Verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[
                    caCertificate: '', 
                    clusterName: 'EKS-1', 
                    contextName: '', 
                    credentialsId: 'k8-token', 
                    namespace: 'webapps', 
                    serverUrl: 'https://EC74F1F36DBFD35119E0E221FA503E41.gr7.ap-south-1.eks.amazonaws.com'
                ]]) {
                    sh '''
                        echo "Verifying deployment..."
                        kubectl get svc -n webapps
                    '''
                }
            }
        }
    }
}
