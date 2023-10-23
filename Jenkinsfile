@Library('JENKINS_SHARED_LIB') _

pipeline {
    agent any
    parameters {
        string(name: 'action', defaultValue: 'create', description: 'Choose create/Delete', 
               allowedValues: 'create\ndelete')
    }
    stages {
        stage('Git checkout') {
        when {expression { param.action =='create'}}

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