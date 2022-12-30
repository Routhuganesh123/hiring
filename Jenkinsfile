pipeline {
    agent any

    stages {
      stage('maven build') {
            steps {
                sh "mvn clean package"
                  }
            }
      stage('Docker Build') {
            steps {
                sh "docker build -t routhu0075/hiring:${env.BUILD_NUMBER} ."
            }
        }
      stage('Docker Push') {
           steps {
               withCredentials([string(credentialsId: 'docker-hub', variable: 'hubPwd')]) {
                   sh "docker login -u routhu0075 -p ${hubPwd}"
                   sh "docker push routhu0075/hiring:${env.BUILD_NUMBER}"
               } 
            }
        }
      stage('Docker Deploy') {
           steps {
              sshagent(['docker-cred']) {
                     sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.42.164 docker rm -f hiring"  
                     sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.42.164 docker run -d -p 8080:8080 --name hiring routhu0075/hiring:${env.BUILD_NUMBER}"
                    }
               } 
            }
        }
    }
