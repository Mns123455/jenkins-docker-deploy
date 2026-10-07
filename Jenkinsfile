pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git(
                    branch: 'main',
                    credentialsId: 'github-token',
                    url: 'https://github.com/Mns123455/jenkins-docker-deploy.git'
                )
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t jenkins-docker-deploy .'
            }
        }

        stage('Remove Old Container') {
            steps {
                sh 'docker rm -f jenkins-docker-container || true'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker run -d -p 5000:5000 --name jenkins-docker-container jenkins-docker-deploy'
            }
        }

        stage('Check Running Container') {
            steps {
                sh 'docker ps'
            }
        }

        stage('Application Test') {
            steps {
                sh 'curl http://localhost:5000'
            }
        }

        stage('Logs') {
            steps {
                sh 'docker logs --tail 50 jenkins-docker-container'
            }
        }
    }
}
