

pipeline {
    agent any

    environment {
        MINIKUBE_HOME = 'C:\\Users\\uppar'
        KUBECONFIG = 'C:\\Users\\uppar\\.kube\\config'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code is checked out from GitHub'
            }
        }

        stage('Validate Application') {
            steps {
                bat 'git --version'
                bat 'if not exist index.html exit /b 1'
                bat 'if not exist Dockerfile exit /b 1'
                bat 'if not exist deployment.yaml exit /b 1'
                echo 'All required application files are present'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'minikube image build -t lab6-web-app:v1 .'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
                bat 'kubectl rollout status deployment/lab6-web-app --timeout=120s'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'kubectl get deployments'
                bat 'kubectl get pods'
                bat 'kubectl get services'
            }
        }
    }
}
