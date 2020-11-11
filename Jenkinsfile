pipeline {
    agent any

    stages {
        stage('Dev') {
            steps {
                echo 'Building..'
				echo "Will deploy to ${params.BRANCH_NAME}"
            }
        }
        stage('Cert') {
            steps {
                echo 'Testing..'
				echo "Will deploy to ${params.BRANCH_NAME}"
            }
        }
        stage('PROD') {
            steps {
                echo 'Deploying....'
				echo "Will deploy to ${params.BRANCH_NAME}"
            }
        }
    }
}