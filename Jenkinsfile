pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'matthewuyoyo/demo-app'
        DOCKER_CREDENTIALS = 'dockerhub-credentials'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/MatthewUyoyo/java-maven-app.git', branch: 'master'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build and Push') {
            steps {
                script {
                    docker.withRegistry('', "${DOCKER_CREDENTIALS}") {
                        def appImage = docker.build("${DOCKER_IMAGE}:latest")
                        appImage.push()
                    }
                }
            }
        }
    }
}
