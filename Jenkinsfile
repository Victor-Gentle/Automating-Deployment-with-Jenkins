pipeline {
    agent any

    stages {
        stage('Connect To Github') {
            steps {
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Victor-Gentle/Automating-Deployment-with-Jenkins.git']])
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t victorgentle/automatewebapp-image:latest .'
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker run -itd -p 8081:80 victorgentle/automatewebapp-image:latest'
                }
            }
        }
        stage('Push Docker image') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u victorgentle -p ${dockerhubpwd}'
}
                    sh 'docker push victorgentle/automatewebapp-image:latest'
                }
            }
        }
    }
}
