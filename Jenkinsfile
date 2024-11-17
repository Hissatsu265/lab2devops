pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // Lấy mã nguồn từ repository
                git branch: 'main', url: 'https://github.com/Hissatsu265/lab2devops.git'
            }
        }

        stage('Build and Deploy service1') {
            steps {
                dir('service1') {
                    // Build Docker image cho service1
                    sh 'docker build -t service1-backend .'

                    // Dừng và xoá container cũ (nếu tồn tại)
                    sh 'docker stop service1-container || true && docker rm service1-container || true'

                    // Chạy container mới cho service1
                    sh 'docker run -d -p 5000:5000 --name service1-container service1-backend'
                }
            }
        }

        stage('Build and Deploy service2') {
            steps {
                dir('service2') {
                    // Build Docker image cho service2
                    sh 'docker build -t service2-backend .'

                    // Dừng và xoá container cũ (nếu tồn tại)
                    sh 'docker stop service2-container || true && docker rm service2-container || true'

                    // Chạy container mới cho service2
                    sh 'docker run -d -p 5001:5001 --name service2-container service2-backend'
                }
            }
        }
    }
}
