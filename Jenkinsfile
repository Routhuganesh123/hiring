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
                echo "deploying to dev"
            }
        }
      stage('tomcat deploy -prod') {
            when {
                branch 'main'
                 }
            steps {
                echo "deploying to production"
            }
        }
    }
}
