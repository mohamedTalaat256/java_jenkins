pipeline {
    // Restricts the pipeline to run only on a Windows agent
    agent { label 'windows' }

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
                // Changed from 'sh' to 'bat' since this runs on a Windows agent
                bat 'mvn clean package'
            }
        }

        stage('Deploy Locally') {
            steps {
                // Uses Windows bat and double quotes to handle spaces in 'Program Files'
                bat 'copy "target\\demo-0.0.1-SNAPSHOT.war" "C:\\Program Files\\Apache Software Foundation\\Tomcat 11.0_Tomcat11-spring-app\\webapps\\app.war"'
            }
        }
    }
}
