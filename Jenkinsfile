pipeline {

    agent any

    environment {
        APP_NAME = 'cicd-demo'
    }

    parameters {
        choice(
            name: 'ENVIRONMENT',
            choices: ['dev', 'stage', 'prod'],
            description: 'Select deployment environment'
        )
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code'
            }
        }

        stage('Build') {
            steps {
                echo "Building ${APP_NAME}"
                sh 'chmod +x app.sh'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests'
                sh './app.sh'
            }
        }

        stage('Deploy DEV') {
            when {
                expression {
                    params.ENVIRONMENT == 'dev'
                }
            }

            steps {
                echo 'Deploying to DEV'
            }
        }

        stage('Deploy STAGE') {
            when {
                expression {
                    params.ENVIRONMENT == 'stage'
                }
            }

            steps {
                echo 'Deploying to STAGE'
            }
        }

        stage('Production Approval') {
            when {
                expression {
                    params.ENVIRONMENT == 'prod'
                }
            }

            steps {
                input(
                    message: 'Deploy to production?',
                    ok: 'Deploy'
                )
            }
        }

        stage('Deploy PROD') {
            when {
                expression {
                    params.ENVIRONMENT == 'prod'
                }
            }

            steps {
                echo 'Deploying to PRODUCTION'
            }
        }
    }

    post {

        success {
            echo 'Pipeline completed successfully'
        }

        failure {
            echo 'Pipeline failed'
        }

        always {
            echo 'Pipeline execution finished'
        }
    }
}

