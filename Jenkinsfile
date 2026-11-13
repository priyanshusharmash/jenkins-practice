pipeline {
    agent any

    stages {
        stage("Checkout") {
            steps {
                checkout scm
            }
        }

        stage("Build Docker Image") {
            steps {
                bat "docker build -t jenkins-practice:${BUILD_NUMBER} -f Dockerfile ."
            }
        }

        stage("Destroy previous container") {
            steps {
                bat 'docker rm -f jenkins-practice || exit /b 0'
            }
        }

        stage("Start new container") {
            steps {
                bat "docker run -d --name jenkins-practice -p 8080:80 jenkins-practice:${BUILD_NUMBER}"
            }
        }

        stage("Remove old images") {
            steps {
                bat "docker image prune -f"
            }
        }
    }
}
