pipeline {
    pipeline {
    agent any

    environment {
        DOCKER_IMAGE = matthewuyoyo/demo-app
        REPO_URL = "https://github.com/MatthewUyoyo/Java-maven-app.git"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: "${REPO_URL}"
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    docker.image("${DOCKER_IMAGE}").run('-d -p 8081:8080')
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
