pipeline {
    agent any

    tools {
        maven 'maven-3.9'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/MatthewUyoyo/Java-maven-app.git', branch: 'master'
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    dockerImage = docker.build("java-maven-app:latest")
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    dockerImage.run('-p 8081:8080')
                }
            }
        }
    }
}
