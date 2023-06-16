pipeline {
    agent any
    tools {
      jdk 'java'
      maven 'my-maven'
    }

    stages {
        stage("cleanup workspace") {
            steps{
                cleanWs()
            }
        }
        stage("checkout from scm") {
            steps {
                git branch: 'main', url: 'https://github.com/jobsforprabu/maven-web-app'
            }
        }
        stage("Build Application") {
            steps {
                sh "mvn clean package"
            }
        }
        stage("Test Application") {
            steps {
                sh "mvn test"
            }

        }
    }
    
}