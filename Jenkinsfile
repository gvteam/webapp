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
		
		    stage ('Check-Git-Secrets') {
      steps {
        sh 'rm trufflehog || true'
        sh 'docker run gesellix/trufflehog --json https://github.com/gvteam/webapp.git > trufflehog'
        sh 'cat trufflehog'
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
                sh 'scp -o StrictHostKeyChecking=no target/*.war root@159.65.152.164:/opt/tomcat/latest/webapps/webapp.war'
              }      
           }       
    }
	}
}
