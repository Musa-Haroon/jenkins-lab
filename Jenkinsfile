pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Musa-Haroon/jenkins-lab.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("jenkins-lab:latest")
                }
            }
        }

        stage('Run Docker Image') {
            steps {
                script {
                    docker.run("--name my-jenkins-app jenkins-lab:latest")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerHubCred') {
                        dockerImage.push("latest")
                    }
                }
            }
        }
    }
}