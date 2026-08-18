pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps { git branch: 'main', url: 'https://github.com/Shreyaa-Mishraa/jenkins-cicd-demo.git' }
        }
        stage('Install Dependencies') {
            steps { sh 'pip install -r requirements.txt' }
        }
        stage('Build') {
            steps { sh 'docker build -t jenkins-with-git .' }
        }
        stage('Test') {
            steps { sh 'pytest test_app.py' }
        }
        stage('Deploy to Kubernetes') {
            steps { sh 'kubectl apply -f k8s/deployment.yaml -f k8s/service.yaml' }
        }
    }
    post {
        success {
            archiveArtifacts artifacts: 'app.py', fingerprint: true
        }
    }
}
