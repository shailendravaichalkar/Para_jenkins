pipeline {
    agent any

    stages {
        stage('Dev') {
            when {
                // Only say hello if a "greeting" is requested
                expression { params.BRANCH_NAME == 'dev' }
            }
            steps {
                echo "Hello, You are in dev!"
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


			