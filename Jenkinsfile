pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // Lấy mã nguồn từ repository
                git branch: 'main', url: 'https://github.com/Hissatsu265/lab2devops.git'
            }
        }

        stage('Build and Deploy services1') {
            steps {
                dir('services1') {
                    // Build Docker image cho services1
                    sh 'docker build -t services1-backend .'

                    // Dừng và xoá container cũ (nếu tồn tại)
                    sh 'docker stop services1-container || true && docker rm services1-container || true'

                    // Chạy container mới cho services1
                    sh 'docker run -d -p 5000:5000 --name services1-container services1-backend'
                }
            }
        }

        stage('Build and Deploy services2') {
            steps {
                dir('services2') {
                    // Build Docker image cho services2
                    sh 'docker build -t services2-backend .'

                    // Dừng và xoá container cũ (nếu tồn tại)
                    sh 'docker stop services2-container || true && docker rm services2-container || true'

                    // Chạy container mới cho services2
                    sh 'docker run -d -p 5001:5001 --name services2-container services2-backend'
                }
            }
        }
    }
}
