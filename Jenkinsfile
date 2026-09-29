pipeline {
    agent any
    options {
        // Prevents Jenkins from automatically checking out code twice
        skipDefaultCheckout()
    }
    tools {
        maven 'Maven3'
        jdk 'jdk-21'
    }
    stages {
        stage('Clean & Checkout') {
            steps {
                cleanWs() // Clean the workspace first
                checkout scm // Manually fetch code from source control
            }
        }
        stage('Build & Package') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy Locally') {
            steps {
                // Copy and rename the file using Windows Batch (wrapped in double quotes due to spaces in path)
                bat 'copy "target\\demo-0.0.1-SNAPSHOT.war" "C:\\Program Files\\Apache Software Foundation\\Tomcat 11.0_Tomcat11-spring-app\\webapps\\app.war"'

                // Restart the Windows Service
                bat 'net stop Tomcat11-spring-app && net start Tomcat11-spring-app'
            }
        }
    }
}
