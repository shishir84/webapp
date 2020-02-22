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
  }
  
  stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@13.127.108.97:/prod/apache-tomcat-8.5.51/webapps/webapp.war'
              }      
           }       
    }
}
