pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/your-username/node-app.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t node-app .'
            }
        }

        stage('Login DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker tag node-app your-dockerhub-username/node-app'
                sh 'docker push your-dockerhub-username/node-app'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 3000:3000 your-dockerhub-username/node-app'
            }
        }
    }
}