pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/your-repo.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'podman build -t myapp:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                podman stop myapp || true
                podman rm myapp || true
                podman run -d -p 8081:8080 --name myapp myapp:latest
                '''
            }
        }
    }
}
