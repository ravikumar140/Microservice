pipeline {
    agent any

    stages {
        stage('Deploy To K8s') {
            steps {
                withKubeCredentials(credentialsId: 'your-kube-credentials-id', namespace: 'webapps') {
                    sh "kubectl apply -f deployment-service.yml"
                    sleep 60
                }
            }
        }
        
        stage('Verify Deployment') {
            steps {
                withKubeCredentials(credentialsId: 'your-kube-credentials-id', namespace: 'webapps') {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
