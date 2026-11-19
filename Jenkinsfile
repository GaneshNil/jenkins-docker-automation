pipeline {
    agent { label 'docker-agent' }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Verify Files') {
            steps {
                sh '''
                    echo "Checking project files..."
                    ls -la
                    test -f app.py
                    test -f Dockerfile
                    test -f requirements.txt
                    echo "All project files found!"
                '''
            }
        }
    }

    post {
        success {
            echo 'GitHub checkout successful!'
        }
        failure {
            echo 'Pipeline failed. Check console output.'
        }
    }
}
