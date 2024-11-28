pipeline {
    agent any

    environment {
        KUBECONFIG = '/var/lib/jenkins/.kube/config'  // Ensure the correct Kubeconfig path
    }

    stages {
        stage('Deploy To K8s') {
            steps {
                script {
                    // Ensure kubectl is set up correctly with Kubeconfig path
                    withKubeCredentials([kubeConfig: KUBECONFIG]) {
                        // Apply Kubernetes manifest
                        sh "kubectl apply -f deployment-service.yml"
                        sleep 60 // Optional: Adjust time based on your application startup time
                    }
                }
            }
        }
        
        stage('Verify Deployment') {
            steps {
                script {
                    // Verify deployment status
                    withKubeCredentials([kubeConfig: KUBECONFIG]) {
                        sh "kubectl get svc -n webapps"
                    }
                }
            }
        }
    }
}
