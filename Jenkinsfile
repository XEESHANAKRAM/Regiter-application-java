pipeline {
    agent any
    tools {
        jdk 'Java'
        maven 'Maven3'
    }
    environment {
	    APP_NAME = "register-app-pipeline"
        RELEASE = "1.0.0"
        DOCKER_USER = "xeeshanakram"
        DOCKER_PASS = 'Risk@@8080'
        IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
    }    
    stages {
        stage ("Clean workspace") {
            steps{
                cleanWs()
            }
        }
        
        stage ("Checkout From SCM") {
            steps{
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/XEESHANAKRAM/Regiter-application-java'
            }
        }
        stage ("Build Application") {
            steps{
                sh "mvn clean package"
            }
        }
        stage ("Test Application") {
            steps {
                sh "mvn test"
            }
        }
        stage ("Sonarqube-scanner") {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'jenkins-sonar') {
                        sh "mvn sonar:sonar"
                    }
                }
            }
        }
        stage ("Build and Push Docker Image") {
            steps {
                script {
                   docker.withRegistry('',DOCKER_PASS) {
                        docker_image = docker.build "${IMAGE_NAME}"
                    }
                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image.push("${IMAGE_TAG}")
                        docker_image.push('latest')
                    }

                }
            }
        }
        
    }
}
