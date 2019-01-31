pipeline {
	agent any
    stages {
         stage('Build') {
		 agent {docker { image 'maven:3.6.0-alpine' } }             
            steps {		
                 git credentialsId: 'GitHub', url: 'https://github.com/poojasree/InformationCentre.git'
                sh 'mvn -X clean install'      
            }
        } 
		stage('Helm') {
		   
            steps {		
                    sh 'helm init'   
					sh 'helm create Info_Chart'
					   
            }
        } 
         
    }
}
