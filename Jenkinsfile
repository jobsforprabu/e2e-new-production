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
                git branch: 'main', url: 'https://github.com/jobsforprabu/e2e-new-production'
            }
        }
    }
    
}