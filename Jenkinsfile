pipeline {
    agent any
    stages {

    if (isUnix()) {
            stage('Build test code') {
                steps {
                    sh 'mvn clean install -DskipTests'
                }
            }
            stage('Execute test') {
                steps {
                    sh 'mvn test'
                }
            }
        else {
            stage('Build test code') {
                    steps {
                        bat 'mvn clean install -DskipTests'
                    }
                }
                stage('Execute test') {
                    steps {
                        bat 'mvn test'
                    }
                }
        }
        stage('Generate allure report') {
            steps {
                script {
                    allure([
                            includeProperties: false,
                            jdk              : '',
                            properties       : [],
                            reportBuildPolicy: 'ALWAYS',
                            results          : [[path: 'target/allure-results']]
                    ])
                }
            }
        }
    }
}