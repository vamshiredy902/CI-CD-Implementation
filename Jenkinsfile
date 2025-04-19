pipeline {
    agent any

    tools {
        maven 'Maven3' // configure this name in Jenkins > Global Tools Configuration
    }

    environment {
        IMAGE_NAME = "vamshi589/simple-java-cicd"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/your-username/simple-java-cicd.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:${BUILD_NUMBER}")
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                withDockerRegistry([ credentialsId: 'dockerhub-creds', url: '' ]) {
                    script {
                        docker.image("${IMAGE_NAME}:${BUILD_NUMBER}").push()
                    }
                }
            }
        }

        stage('Clean up') {
            steps {
                sh 'docker rmi ${IMAGE_NAME}:${BUILD_NUMBER} || true'
            }
        }
    }
}
