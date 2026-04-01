pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'gestion-produits'
        DOCKER_TAG = "${BUILD_NUMBER}"
    }

    tools {
        maven 'Maven-3.9.0'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn clean verify'
            }
        }

        stage('Docker Build') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
                sh "docker tag ${DOCKER_IMAGE}:${DOCKER_TAG} ${DOCKER_IMAGE}:latest"
            }
        }
    }

    post {
        success {
            echo 'Build SUCCESS! Coverage ≥ 80%'
        }
        failure {
            echo 'Build FAILED!'
        }
    }
}