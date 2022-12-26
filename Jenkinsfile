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
                sh "docker build -t routhu0075/hiring:0.0.2 ."
            }
        }
      stage('Docker Push') {
           steps {
                sh "docker login -u routhu0075 -p Ganesh0075"
                sh "docker push routhu0075/hiring:0.0.2"
            }
        }
    }
}
