pipeline {
    agent any

    environment {
        SONARQUBE = 'sonar-server'   // Name you will configure in Jenkins
        DOCKER_IMAGE = 'project10-app'
    }

    stages {

        stage('Pull Code') {
            steps {
                git branch: 'main', url: 'https://github.com/<your-username>/project-10.git'
            }
        }

        stage('SonarQube Code Analysis') {
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh 'sonar-scanner'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t project10-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    docker rm -f project10-app || true
                    docker run -d -p 8082:80 --name project10-app project10-app
                '''
            }
        }
    }
}
