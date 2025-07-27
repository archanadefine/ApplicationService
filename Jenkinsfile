pipeline {
    agent any

    tools {
        maven 'maven'   // Jenkins Maven installation name
        jdk 'jdk-21'    // Jenkins JDK installation name
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
        stage('Run Tests Pipeline') {
            steps {
                script {
                    echo "Triggering MyGitPipelineJob..."
                    def result = build job: 'MyGitPipelineJob',
                                       wait: true,
                                       propagate: true // fails this job if test job fails
                    echo "Test pipeline finished successfully."
                }
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
