pipeline {
    environment {
    registry = "fpereyra/node-images"
    registryCredential = 'dockerhub'
    dockerImage = ''
    }

    agent any
    stages {
            stage('Cloning our Git') {
                steps {
                git 'https://github.com/fpereyrap/jenkins-test'
                }
            }
            
            stage('test') {
                steps {
                    sh 'ls -la'
                }
            }

            stage('validate Dockerfile') {
                steps {
                    sh 'docker run --rm -i --env HADOLINT_OVERRIDE_WARNING=DL3010 --env HADOLINT_NOFAIL=1 hadolint/hadolint < Dockerfile'
                    // sh 'docker run --rm -i hadolint/hadolint < Dockerfile'
                }
            }
            
            stage('Building Docker Image') {
                steps {
                    script {
                        def newApp = docker.build registry + ":$BUILD_NUMBER"
                        docker.withRegistry('', registryCredential) {
                        newApp.push()
                        }
                        // newApp.push()
                    }
                }
            }
        }
    }