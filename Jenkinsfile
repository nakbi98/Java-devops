@Library('JENKINS_SHARED_LIB') _

pipeline {
    agent any
    parameters {
        choice(name: 'action', choices: ['create', 'delete'], description: 'Choose create/Delete')
        string(name: 'ImageName', description:"name of the docker build", defaultValue:'javapp')
        string(name: 'ImageTag', description:"tag of the docker build", defaultValue:'v1')
        string(name: 'AppName', description:"name of the Application", defaultValue:'springboot')

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
                def SonarQubecredentialsId ='sonarqube-api'
                    StatiCodeAnalysis(SonarQubecredentialsId)
                }
            }
        }
        stage('Quality Gate Status chek:sonarqube') {
            when {expression { params.action =='create'}}
            steps {
                script {
                def SonarQubecredentialsId ='sonarqube-api'
                    StatiCodeAnalysis(SonarQubecredentialsId)
                }
            }
        }
        stage('maven Build') {
            when {expression { params.action =='create'}}
            steps {
                script {
                 mvnBuild() 
                }
            }
        }
        stage('Docker Image Build') {
            when {expression { params.action =='create'}}
            steps {
                script {
                 dockerBuild("${params.ImageName}","${params.ImageTag}","${params.AppName}") 
                }
            }
        }
                
        
    }
}