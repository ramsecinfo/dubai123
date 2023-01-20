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

    stage ('Build') {
      steps {
      sh 'mvn clean package'
       }
    }
stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['ubuntu']) {
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@ip-172-31-91-113:/devsec/apache-tomcat-9.0.71/webapps/webapp.war'


    }
}
}
  }
}
