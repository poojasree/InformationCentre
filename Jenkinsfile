pipeline {
    agent none
    stages {
         stage('Build') {
		   agent {
                docker { image 'pooja1989/maven:v1.1' }
           }
            
            steps {
			   
                git credentialsId: 'GitHub', url: 'https://github.com/poojasree/InformationCentre.git'
                sh 'mvn clean install'
            }
         }
         stage('Nexus Uploading') {
		   agent {
                docker { image 'pooja1989/maven:v1.1' }
           }
            
            steps {
                
                sh 'curl -u build_user:build_pwd --upload-file "$WORKSPACE/target/InformationCentre.war" http://52.173.28.7:8081/repository/maven-releases/POC3TEAMC/InformationCentre/$BUILD_NUMBER/InformationCentre-$BUILD_NUMBER.war'
            }
         }
        
		
         stage('Tomcat') {
            agent any
            steps {
                sh 'docker build -t tomcat .'
                sh 'docker tag tomcat pooja1989/tomcat:$BUILD_NUMBER'
                withCredentials([usernamePassword(credentialsId: 'Dockerhub', passwordVariable: '', usernameVariable: '')]) {
                sh 'docker push pooja1989/tomcat:$BUILD_NUMBER'
                 }
         }
		 }
        
        }
         }
