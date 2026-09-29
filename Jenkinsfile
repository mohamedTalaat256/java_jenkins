pipeline {
    agent any
    options {
        skipDefaultCheckout()
    }
    tools {
        maven 'Maven3'
        jdk 'jdk-21'
    }
    stages {
        stage('Clean & Checkout') {
            steps {
                cleanWs()
                checkout scm
            }
        }
        stage('Build & Package') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy Remotely') {
            steps {
                // 1. Securely copy (scp) the war file to the Windows machine and rename it
                // Replace 'user@windows-ip' with your actual Windows username and server IP/hostname
                sh 'scp target/demo-0.0.1-SNAPSHOT.war user@windows-ip:"C:/Program Files/Apache Software Foundation/Tomcat 11.0_Tomcat11-spring-app/webapps/app.war"'

                // 2. Restart the Windows service via SSH
                sh 'ssh user@windows-ip "net stop Tomcat11-spring-app && net start Tomcat11-spring-app"'
            }
        }
    }
}
