pipeline {
    agent any

    tools {
        maven 'Maven 3' // Make sure 'Maven 3' is set in Jenkins tools
    }

    stages {
        stage('Clone') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
    }

    post {
        success {
            echo "Build successful!"
        }
        failure {
            echo "Build failed!"
        }
    }
}
