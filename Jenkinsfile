pipeline {
    agent any
    tools{
        maven 'maven3'
    }
    triggers {
  cron 'H/1 * * * *'
}

  options {
  buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '6', numToKeepStr: '10')
  timestamps()
}
  

    stages {
        stage('Clone the repository') {
            steps {
              git credentialsId: 'Github_username_password', url: 'https://github.com/techworldwithmurali/web-application.git' 
            }
        }
        
         stage('Build the code') {
            steps {
             
              sh ' mvn install '  
            }
        }
        
          stage("Deploy the war file to Dev environment"){
            steps{
                deploy adapters: [tomcat7(credentialsId: 'Tomcat_username_password', path: '', url: 'http://44.210.111.25:8080')], contextPath: null, war: '**/*.war'
            }
        }
       

}
post {
  always {
    // One or more steps need to be included within each condition's block.
    slackSend channel: 'dev', message: 'Build is completed', teamDomain: 'techworldwithmurali', tokenCredentialId: 'Slack-dev-token'
  }
}
}