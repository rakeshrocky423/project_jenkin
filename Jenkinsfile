pipeline {
    agent any
    
    tools {
        // Define the Maven tool with the name 'Maven3'
        maven 'Maven3'
    }
        
    stages {
        stage('Build') {
            steps {
                // Execute Maven clean and package commands
                sh 'mvn clean package'
            }
        }
        
        stage('Archive') {
            steps {
                // Archive the built artifact
                archiveArtifacts '**/target/*.war'
            }
        }
        
        stage('Deploy to Tomcat server') {
            steps {
                // Deploy the artifact to Tomcat server
                deploy adapters: [tomcat9(credentialsId: 'username_password_tomcat', path: '', url: 'http://15.206.124.235:8070/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
