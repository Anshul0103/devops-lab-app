
pipeline {

    agent any

    triggers {
        pollSCM('H/2 * * * *')
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out GitHub repository'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building application'

                sh '''
                    test -f app/index.html
                    echo "Application build successful"
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application'

                sh '''
                    grep -q "Welcome to My DevOps Project" app/index.html
                    echo "Application test passed"
                '''
            }
        }

        stage('Deployment Preparation') {
            steps {
                echo 'Application is ready for Ansible deployment'
            }
        }
    }

    post {
        success {
            echo 'CI Pipeline completed successfully!'
        }

        failure {
            echo 'CI Pipeline failed!'
        }
    }
}
