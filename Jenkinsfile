pipeline {
    agent any

    tools {
        maven 'Maven 3.9.6'
    }

    environment {
        DOCKER_IMAGE = "thedevilingninja/devops_ve6:${BUILD_NUMBER}"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/chaitanya566/DevOps_VE6.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-creds']) {
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl set image deployment/sample-app-deployment sample-container=$DOCKER_IMAGE'
            }
        }
    }
}
