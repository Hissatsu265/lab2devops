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
        stage('Test Services') {
            steps {
                script {
                    // Kiểm tra service1
                    def service1Response = sh(
                        script: "curl -s -o /dev/null -w '%{http_code}' http://localhost:5000/",
                        returnStdout: true
                    ).trim()

                    if (service1Response != '200') {
                        error "Service1 API test failed! Expected HTTP 200 but got ${service1Response}"
                    }

                    // Kiểm tra service2
                    def service2Response = sh(
                        script: "curl -s -o /dev/null -w '%{http_code}' http://localhost:5001/",
                        returnStdout: true
                    ).trim()

                    if (service2Response != '200') {
                        error "Service2 API test failed! Expected HTTP 200 but got ${service2Response}"
                    }

                    echo 'All API tests passed!'
                }
            }
        }
    }
}
