pipeline {
	agent any
	tools {
		maven 'maven'
	}
	stages {
		stage ('Initialize') {
		steps {
			sh '''
				echo "PATH=${PATH}"
				echo "M2_HOME = ${M2_HOME}"
				'''
		}
		}

		stage('Build') {
			steps {
			sh 'mvn clean package'
			}
		}
		
		stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
                sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/webapp-cicd-pipeline/target/*.war root@159.65.152.164:/opt/tomcat/apache-tomcat-9.0.31/webapps/webapp.war'
              }      
           }       
    }
	}
}
