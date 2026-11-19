pipeline {
    agent {
        label 'docker-agent'
    }

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
                    test -f app.py
                    test -f Dockerfile
                    test -f requirements.txt
                    echo "All project files found!"
                '''
            }
        }

        stage('Docker Build') {
            steps {
                sh '''
                    echo "Building Docker image..."
                    docker build -t hotel-demo-app:latest .
                    echo "Docker image built successfully!"
                '''
            }
        }
    }

   stage('Docker Deploy') {
    steps {
        sh '''
            echo "Deploying Flask application..."

            docker stop hotel-demo || true
            docker rm hotel-demo || true

            docker run -d \
              --name hotel-demo \
              --restart unless-stopped \
              -p 127.0.0.1:8081:5000 \
              hotel-demo-app:latest

            echo "Deployment completed!"
        '''
    }
}
 post {
        success {
            echo 'Jenkins pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check console output.'
        }
    }
}
