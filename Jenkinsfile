pipeline {
    agent { agent 'jenkins-agent' }
    tools {
        jdk 'Java'
        maven 'Maven'
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
    }
}
