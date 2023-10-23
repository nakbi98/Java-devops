@Library('JENKINS_SHARED_LIB') _

pipeline {
    agent any
    parameters {
        choice(name: 'action', choices: ['create', 'delete'], description: 'Choose create/Delete')
    }
    stages {
        stage('Git checkout') {
        when {expression { params.action =='create'}}

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
            when {expression { params.action =='create'}}
            steps {
                script {
                    mvnTest()
                }
            }
        }
         stage('Integration Test maven') {
            when {expression { params.action =='create'}}
            steps {
                script {
                    mvnIntegrationTest()
                }
            }
        }

        stage('Static Code Analysis:sonarqube') {
            when {expression { params.action =='create'}}
            steps {
                script {
                def SonarQubecredentialsId =  'sonarqube-api'
                    StatiCodeAnalysis(SonarQubecredentialsId)
                }
            }
        }
                
        
    }
}