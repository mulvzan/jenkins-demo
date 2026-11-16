pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code'
            }
        }

        stage('Build') {
            steps {
                sh 'python3 --version'
                sh 'python3 -m compileall -q .'
            }
        }

        stage('Test') {
            steps {
                sh 'python3 -m pip install -r requirements.txt'
                sh 'python3 -m pytest -v'
            }
        }

        stage('Complete') {
            steps {
                echo 'CI Pipeline completed successfully!'
            }
        }
    }
}
