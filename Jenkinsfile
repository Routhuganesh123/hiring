pipeline {
    agent any

    stages {
        stage('Git checkout') {
            steps {
                git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/Routhuganesh123/hiring'
            }
        }
        
        stage('maven build') {
            steps {
                sh "mvn clean package"
            }
        }
        
        stage('tomcat deploy') {
            steps {
                sshagent(['tomcat-cred']) {
                    sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.47.164:/opt/tomcat9/webapps"
                    sh "ssh ec2-user@172.31.47.164 /opt/tomcat9/bin/shutdown.sh"
                    sh "ssh ec2-user@172.31.47.164 /opt/tomcat9/bin/startup.sh"
                }
            }
        }
    }
}
