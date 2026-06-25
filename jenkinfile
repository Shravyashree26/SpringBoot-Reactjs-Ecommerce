pipeline {
    agent any

    stages {

        stage('Build Backend') {
            steps {
                dir('Ecommerce-Backend') {
                    sh 'mvn clean package'
                    sh 'docker build -t ecommerce-backend .'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('Ecommerce-Frontend') {
                    sh 'npm install'
                    sh 'docker build -t ecommerce-frontend .'
                }
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop ecommerce-backend || true
                docker stop ecommerce-frontend || true

                docker rm ecommerce-backend || true
                docker rm ecommerce-frontend || true

                docker run -d --name ecommerce-backend -p 8082:8080 ecommerce-backend

                docker run -d --name ecommerce-frontend -p 5173:5173 ecommerce-frontend
                '''
            }
        }
    }
}
