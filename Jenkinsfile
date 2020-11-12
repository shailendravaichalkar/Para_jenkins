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
                echo 'Deploying in Prod test 2....'
				echo "Will deploy to ${params.BRANCH_NAME}"
            }
        }
    }
}