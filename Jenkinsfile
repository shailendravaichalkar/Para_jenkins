pipeline {
    agent any

    stages {
        stage('Dev') {
            steps {
                echo 'RUNNING: ${params.BRANCH_NAME} : Building in Dev Test 7..'
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
