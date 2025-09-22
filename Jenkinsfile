pipeline {
    agent any

    tools {
        // Utilise le JDK et Maven que tu as configurés dans Jenkins (Global Tool Configuration)
        jdk 'JDK17'         // Remplace par le nom que tu as donné à ton JDK dans Jenkins
        maven 'MAVEN_HOME'      // Remplace par le nom que tu as donné à ton Maven dans Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/balsamrom/studentmanagement'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Tests') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline terminé (succès ou échec)."
        }
        success {
            echo "✅ Build réussi !"
        }
        failure {
            echo "❌ Build échoué !"
        }
    }
}
