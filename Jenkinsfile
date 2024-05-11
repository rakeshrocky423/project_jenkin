pipeline {
    agent any
    tools {
        maven 'Maven3'
    }

    stages {
        stage('Git checkout') {
            steps {
                git changelog: false, credentialsId: 'git_username_password', poll: false, url: 'https://github.com/ArshiyaBegum1/project_jenkin.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    
                    slackSend (
                        color: '#36a64f', // Green color for success
                        message: 'Build successful! :tada:',
                    )
                }
            }
        
        }
        stage('Deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat_newusername_password', path: '', url: 'http://3.85.1.31:8080')], contextPath: null, war: '**/*.war'
            }
            post {
                success {
                    
                    // Send Slack notification
                    slackSend (
                        color: '#36a64f', // Green color for success
                        message: 'Deployment successful! :tada:',
                    )
                }
            }
        }
        
    }
}

