pipeline {
    agent any

    parameters {
        // parameters here
    }

    environment {
        // environment variables here
    }

    options {
        // pipeline options here
    }

    stages {

        stage('SCM Pull') {
            steps {
                git branch: 'main', url: 'https://github.com/travis2319/podinfo.git', credentialsId: 'travis2319-github'
            }
        }

        stage('Build') {
            steps {
            }
        }

        stage('SAST Check') {
            steps {
            }
        }

        stage('OWASP Dependency Check') {
            steps {
            }
        }

        stage('Build Docker Image') {
            steps {
            }
        }

        stage('Push to Docker Registry') {
            steps {
            }
        }

        stage('Deploy') {
            steps {
            }
        }
    }

    post {
        always {
        }
        success {
        }
        failure {
        }
    }
}