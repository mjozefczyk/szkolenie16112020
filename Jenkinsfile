pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/testautomation112020/qa.git'
            }

        }
        stage('run') {
                    steps {

                        // Run Maven on a Unix agent.
                        sh "mvn -Dmaven.test.failure.ignore=true clean install"

                        // To run Maven on a Windows agent, use
                        // bat "mvn -Dmaven.test.failure.ignore=true clean package"
                    }

                }
        stage('report') {
            steps {
                script {
                        allure([
                                includeProperties: false,
                                jdk: '',
                                properties: [[key: 'allure.issues.tracker.pattern', value: 'http://tracker.company.com/%s'],
                                [key: 'allure.tests.management.pattern', value: 'http://tms.company.com/%s']],
                                reportBuildPolicy: 'ALWAYS',
                                results: [[path: 'target/allure-results']]
                        ])
                }
                }
        }
    }
}
