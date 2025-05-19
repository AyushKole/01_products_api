pipeline {
    agent any
    
    tools {
        maven "maven-3.9.9"
    }

    
    stages {
        stage('git clone') {
            steps {
                git branch: 'main', url: 'https://github.com/ashokitschool/01_products_api.git'
            }
        }

        stage('maven build'){
            steps{
                sh 'mvn clean package'
            }
        }
        
        stage('Build Docker Image'){
            steps{
                sh 'docker build -t ashokit/products .'
            }
        }
        stage('Push Docker Image'){
            steps{
                withCredentials([string(credentialsId: 'dockerloginpwd', variable: 'docker_login_pwd')]) {
                    sh 'docker login -u ayushkole45 -p ${docker_login_pwd}'
                    sh 'docker push ashokit/products'
                }
            }
        }
        stage('K8S Deployment'){
            steps{
                sh 'kubectl apply -f Deployment.yml'
            }
        }
    }
}

