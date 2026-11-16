pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code checked out from GitHub'
            }
        }

        stage('Build') {
            steps {
                sh '''
                    python3 --version
                    python3 -m compileall -q .
                    python3 -m venv .venv
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    .venv/bin/pip install -r requirements.txt
                    .venv/bin/python -m pytest -v
                '''
            }
        }
        stage('Docker Build') {
            steps {
                sh '''
                    docker build \
                        -t jenkins-demo:${BUILD_NUMBER} \
                        -t jenkins-demo:latest .
                    
                    docker images jenkins-demo
                '''
            }
        }
        stage('Docker Run') {
            steps {
                sh '''
                    docker run --rm jenkins-demo:${BUILD_NUMBER}
                '''
            }
        }
        
        
        stage('Complete') {
            steps {
                echo 'CI Pipeline completed successfully!'
            }
        }
    }
}
