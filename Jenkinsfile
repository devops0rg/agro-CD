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

    
       stage('SonarQube Analysis') {
        steps{
           script{
          withSonarQubeEnv(credentialsId: 'sonar1') { 
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
                //sh 'docker tag samplewebapp nikhilnidhi/samplewebapp:$BUILD_NUMBER'
               
          }
        }
       stage('Publish image to Docker Hub') {
          
    steps {
       withCredentials([string(credentialsId: 'dockerhubpass', variable: 'dockerhubcred')]) {
                   sh 'docker login -u navyaa14 -p ${dockerhubcred}'
          sh  'docker push navyaa14/samplewebapp:latest'
        //  sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
}
         stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 navyaa14/samplewebapp"
 
            }
        }

    }
}
