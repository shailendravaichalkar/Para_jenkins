pipeline {
    agent any

    stages {
        stage('Dev') {
            steps {
                echo 'RUNNING: DEV : Building in Dev Test 6..'
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
                echo 'Deploying....'
				echo "Will deploy to ${params.BRANCH_NAME}"
            }
        }
    }
}