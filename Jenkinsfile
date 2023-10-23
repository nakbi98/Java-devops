@Library('JENKINS_SHARED_LIB') _

pipeline{
    agent any
    stages{
        stage('Git checkout'){
            steps{

                script{ 

                   gitCheckout(
                    branch: "main",
                    url: "https://github.com/nakbi98/Java-devops.git"
                   )
                }
            }
        }
    }

     
        stage('Unit Test maven'){
            steps{

                script{ 
                 mvnTest()
                  
                }
            }
        }
    
}