pipeline {
    agent any{
    trigger{
        pollSCM('H/2 * * * *')
    }
    stages{
        stage ('checkout'){
            steps{
                echo 'Checking out github repository...'
                checkout scm
            }
        }    
        stage('Build'){
        steps{
            echo 'Building application'
            sh '''
                test -f app/index.html
                echo 'Applicaiton build successfully...'
            '''
        }
        }
        stage ('Deployment preparation'){
            steps{
                echo 'Application is ready for ansible deployment'
            }
        
        }
    }
    }

    post {
        success{
            echo 'CI pipeline completed successfully.'
        }

        failure{
            echo 'CI pipeline failed'
        }
    }
    
}