pipeline {
    agent any

    stages {
        stage('Dev') {
            steps {
                echo 'Building in Dev..'
				echo "Will deploy to ${params.BRANCH_NAME}"
            }
        }
        stage('Cert') {
            steps {
                echo 'Testing..'
				echo "Will deploy to ${params.BRANCH_NAME}"
            }
        }
        stage('Prod') {
            steps {
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }
                echo "Will deploy to ${params.BRANCH_NAME}"
            }
        }
    }
}