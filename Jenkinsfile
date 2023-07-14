pipeline {
    agent any
  
    stages{
        stage('SCM Checkout'){
          steps{
             git credentialsId: 'git', url: 'https://github.com/BalajiiBharath/CI-CD-using-Docker_nb.git'
           }
        }
   stage('Build Maven'){
            steps{
               script{
              def mavenHome =  tool name: 'maven', type: 'maven'   
              def mavenCMD = "${mavenHome}/bin/mvn"
              sh "${mavenCMD} clean package"
            }
            }
        }
    }
}
