#!/usr/bin/env groovy

pipeline {
    agent any
        options{
            ansiColor('xterm')
        }
        
        tools{
            nodejs 'nodejs-15.14.4'
        }
        stages {
            stage('Setup') {
                steps {
                    sh 'npm install'
                }
            }
            stage('Build') {
                steps {
                    sh 'npm run test'
                }
                post{
                    success{
                        archiveArtifacts 'coverage/*.json'

                    }
                }
            }
            stage('test-ci') {
                steps {
                    sh 'npm run ci-test'
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
