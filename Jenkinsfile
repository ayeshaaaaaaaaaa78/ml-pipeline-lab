pipeline {
    agent any
    stages {
        stage('Fetch Data') {
            steps {
                sh 'git pull origin main'
            }
        }
        stage('Train Model') {
            steps {
                sh 'pip install -r requirements.txt --break-system-packages'
                sh 'python train.py'
            }
        }
        stage('Build Docker') {
            steps {
                sh 'sudo docker build -t ml-pipeline .'
            }
        }
        stage('Run Docker') {
            steps {
                sh 'sudo docker stop ml-pipeline || true'
                sh 'sudo docker rm ml-pipeline || true'
                sh 'sudo docker run -d -p 8000:8000 --name ml-pipeline ml-pipeline'
            }
        }
    }
}
