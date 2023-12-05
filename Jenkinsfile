pipeline {
    agent any

    environment {
        ESCAPE_APPLICATION_ID = credentials('ESCAPE_APPLICATION_ID')
        ESCAPE_API_KEY = credentials('ESCAPE_API_KEY')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm // Checkout the codebase from the SCM provider
            }
        }
        
        stage('Post-Deploy') {
            when {
                branch 'staging' // Only run on the 'staging' branch
            }

            steps {
                script {
                    // Install the Escape CLI tool
                    sh 'npm install -g @escape.tech/action'
                    
                    // Show the installed Escape CLI version
                    sh 'npm show @escape.tech/action version'
                    
                    // Run Escape action
                    sh 'escape-action'
                }
            }

            post {
                always {
                    // Configuration to allow failure
                }
            }
        }
    }
}
