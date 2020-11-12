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
                expression { params.BRANCH_NAME == 'main' }
            }
            steps {
                echo 'Testing..'
				echo "Will deploy to ${params.BRANCH_NAME}"
            }
        }
        stage('Prod') {
            when {
                expression { params.BRANCH_NAME == 'master' }
            }
            steps {
                echo "Hello, You are in PROD!"
                echo 'Deploying....'
				echo "Will deploy to ${params.BRANCH_NAME}"
            }
        }
    }
}


			