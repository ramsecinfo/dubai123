pipeline {
  agent any 
  tools {
    maven 'maven'
  }
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
    
    stage ('Check-Git-Secrets') {
		    steps {
	        sh 'rm trufflehog || true'
		sh 'docker pull gesellix/trufflehog'
		sh 'docker run -t gesellix/trufflehog --json https://github.com/ramsecinfo/dubai123.git > trufflehog'
		sh 'cat trufflehog'
	    }
	    }
	  
	 

    stage ('Build') {
      steps {
      sh 'mvn clean package'
       }
    }
   
    
    stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@3.83.238.126:/devsec/apache-tomcat-9.0.71/webapps/webapp.war'

     }
    }
  }
 }
}

