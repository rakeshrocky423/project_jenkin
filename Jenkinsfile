pipeline {
    agent any
    tools {
        maven 'Maven3'
    }
        
    stages {
        stage ('build') {
            steps {
                sh 'mvn clean package'
            }    
            post {
                success {
                    echo "archiving the artifacts"
                    archiveArtifacts artifacts '**/target/9.war'
                }
            }

        }
        stage ('deploy to tomcat server') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'username_password_tomcat', path: '', url: 'http://15.206.124.235:8070/')], contextPath: null, war: '**/*.war'
            }
        }
    }
    
}   

