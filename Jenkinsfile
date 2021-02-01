#!/usr/bin/env groovy

pipeline {
    agent any
        stages {
            stage('Setup') {
                steps {
                    nodejs(nodeJSInstallationName: 'nodejs-6.14.10') {
                        sh 'npm install'
                    }
                }
            }
            stage('Build') {
                steps {
                    nodejs(nodeJSInstallationName: 'nodejs-6.14.10') {
                        sh 'npm run test'
                    }
                }
                post{
                    success{
                        archiveArtifacts 'coverage/*.json'
                    }
                }
            }
        }
}
