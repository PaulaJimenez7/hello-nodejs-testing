#!/usr/bin/env groovy

pipeline {
    agent any
        options{
            ansiColor('xterm')
        }
        
        tools{
            nodejs 'nodejs-14.15.4'
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
                    always{
                        archiveArtifacts 'test.tap'
                        step([$class: "TapPublisher", testResults: "test.tap"])
                        step([
                            $class: 'CloverPublisher',
                            cloverReportDir: 'coverage',
                            cloverReportFileName: 'clover.xml',
                            healthyTarget: [methodCoverage: 70, conditionalCoverage: 80, statementCoverage: 80],    
                            unhealthyTarget: [methodCoverage: 50, conditionalCoverage: 50, statementCoverage: 50],
                            failingTarget: [methodCoverage: 0, conditionalCoverage: 0, statementCoverage: 0] 
                        ])
                    }
                }
            }
        }
}
