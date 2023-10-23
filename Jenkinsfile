@Library('JENKINS_SHARED_LIB') _

pipeline {
    agent any
    parameters{
        choice(name: 'action', choice: 'create\ndelete', description: 'choose create/Destroy')
    }
    stages {
        when {expression { param.action =='create'}}
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
            when {expression { param.action =='create'}}
            steps {
                script {
                    mvnTest()
                }
            }
        }
         stage('Integration Test maven') {
            when {expression { param.action =='create'}}
            steps {
                script {
                    mvnIntegrationTest()
                }
            }
        }

            stage('Static Code Analysis:sonarqube') {
            when {expression { param.action =='create'}}
            steps {
                script {
                    StatiCodeAnalysis()
                }
            }
        }
                
        
    }
}