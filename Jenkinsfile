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
                withCredentials([string(credentialsId: 'samin-docker', variable: 'samindocker')]) {
                    script {  
                        sh "docker login -u adomicarts -p '${samindocker}'"
                    }
                }
            }
        }
        stage('Push Image') {
            steps {
                sh "docker push lathini/nodeapp-4088:${BUILD_NUMBER}"
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}