pipeline {
    agent any

    stages {
      stage('maven build') {
            steps {
                sh "mvn clean package"
                  }
            }
      stage('Docker build') {
            steps {
                sh "docker run -d -p routhu0075/hiring:0.0.2 ."
            }
        }
      stage('Docker push') {
           steps {
                sh "docket login -u routhu0075 -p Ganesh0075"
                sh "Docker push"
            }
        }
    }
}
