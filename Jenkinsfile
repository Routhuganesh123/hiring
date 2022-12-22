pipeline {
    agent any

    stages {
       
        stage('maven build') {
            when {
                branch 'develop'
            }
            steps {
                sh "mvn clean package"
            }
        }
        
        stage('tomcat deploy -dev') {
            when {
                branch 'develop'
            }
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
