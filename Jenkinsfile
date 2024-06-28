pipeline {
  agent any 
  tools{
      maven 'mvn'}
 stages{
  stage('checkout'){
    steps{
	 checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ggutu/devops-automation-you.git']])
	}
    }
	stage('maven build'){
    steps{
	sh "mvn clean install" 
	}
    }
	stage('docker build image'){
    steps{
	 script{
	  sh  'docker build -t gizachewgutu/devops-integration .'
	   }
	}
    }
    stage('docker push'){
    steps{
	 script{
	 withCredentials([string(credentialsId: 'dockerHub-pwd', variable: 'dockerHubPWD')]) {
	     sh 'docker login -u gizachewgutu -p ${dockerHubPWD}'
	     sh 'docker push gizachewgutu/devops-integration'
}
	   }
	}
    }
 }
 }
  
  
