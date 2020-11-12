// ***********************
//
// Build and deploy different environments with jenkins pipeline
//
// Merge to develop -> triggers development release
// Merge to master without tag -> triggers staging release
// Merge to master with tag -> triggers staging and production release
// Production release requires manual approval on the jenkins job
// 
// Configure jenkins pipeline project to pull tags! By default, tags are not pulled!
// -> Check "Advanced clone behaviours" feature of jenkins git plugin
//
// ***********************


pipeline {
    agent any

    environment {
        GLOBAL_ENVIRONMENT = 'NO_DEPLOYMENT'

        // Need the staging properties anyway to deploy to staging and production simultaneously when doing a prod release
        ENVIRONMENT_STAGING = 'staging'
    }

    triggers {
        pollSCM('H/5 * * * *')
    }

    options {
        // Keep maximum 10 archived artifacts
        buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '10'))

        // No simultaneous builds
        disableConcurrentBuilds()
    }

    stages {
        stage('Prepare workspace') {
            steps {
                echo 'Prepare workspace'

                // Clean workspace
                step([$class: 'WsCleanup'])

                // Checkout git
                checkout scm
            }
        }

        stage('Setup environment') {
            steps {
                echo 'Setup environment'
                
                script {
                    // Determine whether this is a test or a staging / production build                    
                    switch (env.BRANCH_NAME) {
                        case 'develop':
                            GLOBAL_ENVIRONMENT = 'test'
                            break
                        case 'master':
                            GLOBAL_ENVIRONMENT = 'staging'
                            break
                        default: 
                            GLOBAL_ENVIRONMENT = 'NO_DEPLOYMENT'
                            break
                    }

                    // Get tag on current branch
                    TAG = sh(returnStdout: true, script: 'git tag --points-at HEAD')

                    if (TAG && GLOBAL_ENVIRONMENT == 'staging') {
                        echo 'Build for production'

                        // Ask user whether master should be builded and deployed to production
                        try {
                            timeout(time: 15, unit: 'MINUTES') {
                                APPROVED = input(
                                    id: 'BuildForProductionInput',
                                    message: 'Build and deploy',
                                    parameters: [
                                        booleanParam(
                                            defaultValue: false,
                                            description: '',
                                            name: 'Build and deploy ' + TAG + ' for production?'
                                        )
                                    ]
                                )

                                if (APPROVED) {
                                    GLOBAL_ENVIRONMENT = 'production'
                                } else {
                                    error 'Build for production aborted'
                                }
                            }
                        } catch (err) {
                            error 'Build for production aborted'
                        }
                    }
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Build ' + GLOBAL_ENVIRONMENT

                script {
                    if (GLOBAL_ENVIRONMENT == 'NO_DEPLOYMENT') {
                        echo 'This is not develop nor master branch and should not be build'
                    } else {
                        build(GLOBAL_ENVIRONMENT)

                        if (GLOBAL_ENVIRONMENT == 'production') {
                            echo 'Additionally, build staging'
                            build(ENVIRONMENT_STAGING)
                        }
                    }
                }
            }
        }

        stage('Archive artifacts') {
            steps {
                echo 'Archive artifacts'

                script {
                    if (GLOBAL_ENVIRONMENT == 'NO_DEPLOYMENT') {
                        echo 'This is not develop nor master branch and should not be archived'
                    } else {
                        // Archive all build artifacts
                        archiveArtifacts artifacts: 'build/*'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy ' + GLOBAL_ENVIRONMENT

                script {
                    if (GLOBAL_ENVIRONMENT == 'NO_DEPLOYMENT') {
                        echo 'This is not develop nor master branch and should not be deployed'
                    } else {
                        deploy(GLOBAL_ENVIRONMENT)

                        if (GLOBAL_ENVIRONMENT == 'production') {
                            echo 'Additionally, deploy staging'
                            deploy(ENVIRONMENT_STAGING)
                        }
                    }
                }
            }
        }
    }
}

def build(ENVIRONMENT) {
}

def deploy(ENVIRONMENT) {
}