pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "Toniaz28/java-todo-list"
        DOCKER_TAG = "latest"
    }

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/Toniaz28/java-todo-list.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $DOCKER_IMAGE:$DOCKER_TAG ."
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds',
                                                 usernameVariable: 'USER',
                                                 passwordVariable: 'PASS')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                }
            }
        }

        stage('Push Image') {
            steps {
                sh "docker push $DOCKER_IMAGE:$DOCKER_TAG"
            }
        }
    }
}
