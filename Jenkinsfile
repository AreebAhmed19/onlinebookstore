pipeline {
    agent any

    tools {
        maven 'Maven 3'
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

        stage('Publish Test Results') {
            steps {
                script {
                    // Avoid pipeline failure if no test reports exist
                    try {
                        junit 'target/surefire-reports/*.xml'
                    } catch (e) {
                        echo "⚠️ No test reports found. Skipping test results publishing."
                    }
                }
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "✅ Build completed successfully!"
        }
        failure {
            echo "❌ Build failed. Please check the logs."
        }
    }
}
