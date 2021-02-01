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
            stage('test-ci') {
                steps {
                    nodejs(nodeJSInstallationName: 'nodejs-6.14.10') {
                        sh 'npm run ci-test'
                    }
                }
                post{
                    success{
                        archiveArtifacts 'test.tap'
                        step([$class: "TapPublisher", testResults: "test.tap"])
                    }
                }
            }
        }
}
