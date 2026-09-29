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
        stage('Checkout') {
            steps {
                // This will now be the ONLY checkout that happens
                checkout scm
            }
        }

        stage('Build & Package') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy Locally') {
            steps {
                sh 'cp target/demo-0.0.1-SNAPSHOT.war /app-deploy/'
            }
        }
    }
}
