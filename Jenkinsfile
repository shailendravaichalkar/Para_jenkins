pipeline {
    agent any

    stages {
        stage('Dev') {
            steps {
                echo 'RUNNING: Dev : Building in Dev Test 5..'
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
