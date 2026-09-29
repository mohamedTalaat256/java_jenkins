pipeline {
    agent any

    tools {
        // These names MUST match the exact names you gave them in Manage Jenkins -> Tools
        maven 'Maven3'
        jdk 'jdk-21'
    }

    stages {
        stage('Checkout') {
            steps {
                // This automatically pulls your code from the configured repository
                checkout scm
            }
        }

        stage('Build & Package') {
            steps {
                // Compiles the code and packages it into a WAR file
                sh 'mvn clean package'
            }
        }

        stage('Deploy Locally') {
            steps {
                // Copies the generated WAR file into your Docker-mapped Windows directory
                sh 'cp target/demo-0.0.1-SNAPSHOT.war /app-deploy/'
            }
        }
    }
}
