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
                sh 'cp target/demo-0.0.1-SNAPSHOT.war /mnt/tomcat_webapps/app.war'
            }
        }
    }
}
