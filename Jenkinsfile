pipeline {
    agent any

    stages {
        stage('Dev') {
            when {
                expression { params.BRANCH_NAME == 'dev' }
            }
            steps {
                echo "Hello, You are in dev!"
            }
        }
        stage('Cert') {
            when {
                expression { params.BRANCH_NAME == 'cert' }
            }
            steps {
                echo 'Testing..'
				echo "Will deploy to ${params.BRANCH_NAME}"
            }
        }
        stage('Prod') {
            when {
                expression { params.BRANCH_NAME == 'prod' }
            }
            steps {
                echo "Hello, You are in PROD!"
				timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }
                echo "Will deploy to ${params.BRANCH_NAME}"
                echo 'Deploying....'
				echo "Will deploy to ${params.BRANCH_NAME}"
            }
        }
    }
}


			