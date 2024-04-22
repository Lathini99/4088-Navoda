pipeline {
    agent any
   
    stages {
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/Lathini99/4088-Navoda.git'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t lathini/nodeapp-4088:${BUILD_NUMBER} .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'nodejs-4088')]) {
                    script {  
                        sh "docker login -u lathini -p '${nodejs-4088}'"
                    }
                }
            }
        }
        stage('Push Image') {
            steps {
                sh "docker push lathini/nodeapp-4088:${BUILD_NUMBER}"
            }
        }
    } // Added closing brace for 'stages' block

    post {
        always {
            sh 'docker logout'
        }
    }
}

