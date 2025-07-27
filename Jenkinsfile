pipeline {
    agent any

    tools {
        maven 'maven' // Replace with the name of your Maven installation in Jenkins
        jdk 'jdk-21'         // Replace with the JDK name in Jenkins (can be jdk-17, jdk-8, etc.)
    }

    environment {
        REPORT_PATH = 'target/surefire-reports/emailable-report.html'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/archanadefine/ApplicationService.git', branch: 'main'
            }
        }

        stage('Build and package') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive Report') {
            steps {
                archiveArtifacts artifacts: "${REPORT_PATH}", allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        failure {
            echo 'Pipeline failed.'
        }
        success {
            echo 'Pipeline succeeded.'
        }
    }
}
