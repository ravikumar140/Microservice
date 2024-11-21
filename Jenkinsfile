pipeline {
    agent any

    stages {
        stage('Deploy To K8s') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-1', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://EC74F1F36DBFD35119E0E221FA503E41.gr7.ap-south-1.eks.amazonaws.com']]) {
                 sh "kubectl apply -f deployment -service.yml"
                 sleep 60
               }
            }
        }
        
        stage('Verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-1', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://EC74F1F36DBFD35119E0E221FA503E41.gr7.ap-south-1.eks.amazonaws.com']]) {
                    sh "kubectl get all -n webapps"    
              }
            }
        }
    }
}
