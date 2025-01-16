# se_poll
pipeline {
    agent any
    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/pjoshi-afk/SE_MAVEN.git', branch: 'main'
            }
        }
        stage('Clean Build') {
            steps {
                script {
                    bat 'mvn clean'
                }
            }
        }
        stage('Install') {
            steps {
                bat 'mvn install'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }
        stage('Package') {
            steps {
                bat 'mvn package'
            }
        }
    }
}


FROM tomcat:9-jdk21
COPY target/*.war /usr/local/tomcat/webapps