pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
			    echo "Building as ${BRANCH_NAME}"
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Test 4 Deploying....'
            }
        }
    }
}