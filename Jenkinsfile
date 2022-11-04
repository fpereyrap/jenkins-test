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
            
            stage('Building Docker Image') {
                steps {
                    script {
                        def newApp = docker.build registry
                        docker.withRegistry('', registryCredential) {
                        newApp.push()
                        }
                        // newApp.push()
                    }
                }
            }
        }
    }