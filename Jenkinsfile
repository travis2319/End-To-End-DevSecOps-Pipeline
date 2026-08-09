pipeline {
    agent any

    parameters {
        choice(
            name: 'BRANCH_NAME',
            choices: ['dev', 'master'],
            description: 'Git branch to build'
        )
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

        stage('SAST - Static Code Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh """
                        ${tool 'SonarScanner'}/bin/sonar-scanner \
                        -Dsonar.projectKey=podinfo \
                        -Dsonar.sources=. \
                        -Dsonar.exclusions=vendor/**,charts/**,**/*_test.go \
                        -Dsonar.host.url=http://sonarqube:9000
                    """
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
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