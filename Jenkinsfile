pipeline {
    agent any
  
    stages{
        stage('SCM Checkout'){
          steps{
             git credentialsId: 'gitbalaji', url: 'https://github.com/devops0rg/agro-CD.git'
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

    
       stage('SonarQube Analysis') {
        steps{
           script{
          withSonarQubeEnv(credentialsId: 'sonar') { 
          def mavenHome =  tool name: 'maven', type: 'maven'   
          def mavenCMD = "${mavenHome}/bin/mvn"
          sh "${mavenCMD} sonar:sonar"
	        }
           }
	    }
       }
        stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp navyaa14/samplewebapp:latest'
                //sh 'docker tag samplewebapp navyaa14/samplewebapp:$BUILD_NUMBER'
               
          }
        }
       stage('Publish image to Docker Hub') {
          
    steps {
       withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
                   sh 'docker login -u navyaa14 -p ${dockerhub}'
          sh  'docker push navyaa14/samplewebapp:latest'
        //  sh  'docker push navyaa14/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
}
        
}
    }
