pipeline {
    agent any
  
    stages{
        stage('SCM Checkout'){
          steps{
             git credentialsId: 'git', url: 'https://github.com/BalajiiBharath/CI-CD-using-Docker_nb.git'
           }
        }
   stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        
    }
}
