pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'MAVEN_HOME'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/balsamrom/studentmanagement'
            }
        }

        stage('Build, Test and Package') {
            steps {
                // Une seule commande pour tout faire
                bat 'mvn clean package'
            }
            post {
                success {
                    junit 'target/surefire-reports/**/*.xml'
                    archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline terminé."
        }
        success {
            echo "✅ Build réussi !"
        }
        failure {
            echo "❌ Build échoué !"
        }
    }
}
