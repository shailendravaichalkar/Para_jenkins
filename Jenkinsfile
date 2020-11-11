pipeline {
    agent any

    stages {
        stage('Dev') {
            steps {
                echo 'Building..'
				echo "Will deploy to ${params.DEPLOY_ENV}"
            }
        }
        stage('Cert') {
            steps {
                echo 'Testing..'
				echo "Will deploy to ${params.DEPLOY_ENV}"
            }
        }
        stage('PROD') {
            steps {
                echo 'Deploying....'
				echo "Will deploy to ${params.DEPLOY_ENV}"
            }
        }
    }
}