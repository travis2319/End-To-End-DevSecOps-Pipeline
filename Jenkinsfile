pipeline {
    agent any

    parameters {
        string(name: 'BRANCH_NAME', defaultValue: 'main', description: 'Git branch to build')
    }

    environment {
        IMAGE_NAME = 'podinfo'
    }

    options {
        timestamps()
    }

    stages {

        stage('SCM Pull') {
            steps {
                git branch: "${params.BRANCH_NAME}", url: 'https://github.com/travis2319/podinfo.git', credentialsId: 'travis2319-github'
            }
        }

        stage('SAST Check') {
            steps {
                echo 'Performing SAST check...'
            }
        }

        stage('OWASP Dependency Check') {
            steps {
                echo 'Performing OWASP Dependency Check...'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
            }
        }

        stage('Push to Docker Registry') {
            steps {
                echo 'Pushing Docker image to registry...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs for details.'
        }
    }
}