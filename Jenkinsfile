pipeline {
    agent any
    tools {
      jdk 'java'
      maven 'my-maven'
    }
    
    environment {
        APP_NAME = "e2e-new-production"
        RELEASE = "1.0.0"
        DOCKER_USER = "prganesh"
        DOCKER_PASS = "dockerhub"
        IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
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
        stage("Build & Push Docker images") {
            steps {
                script {
                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image = docker.build "${IMAGE_NAME}"
                    }
                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image.push("${IMAGE_TAG}")
                        docker_image.push('lastest')
                    }
                }
            }
        }
    }
    
}