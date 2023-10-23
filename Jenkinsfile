@Library('JENKINS_SHARED_LIB') _

pipeline {
    agent any
    stages {
        stage('Git checkout') {
            steps {
                script {
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: 'main']],
                        userRemoteConfigs: [[url: 'https://github.com/nakbi98/Java-devops.git']]
                    ])
                }
            }
        }

        stage('Unit Test maven') {
            steps {
                script {
                    mvnTest()
                }
            }
        }
         stage('Integration Test maven') {
            steps {
                script {
                    mvnIntegrationTest()
                }
            }
        }
    }
}