pipeline {
    agent any

    stages {
        stage('Deploy To K8s') {
            steps {
                withKubeConfig(credentialsId: 'k8-token') {
                    sh "kubectl apply -f deployment-service.yml"
                    sleep 60
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                withKubeConfig(credentialsId: 'k8-token') {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
