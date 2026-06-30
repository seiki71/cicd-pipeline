pipeline {
    agent any

    tools {
        nodejs 'node'
    }

    stages {
        stage('Build') {
            steps {
                sh 'scripts/build.sh'
            }
        }
        stage('Test') {
            steps {
                sh 'scripts/test.sh'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t nodedev:v1.0 .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker stop app_dev || true'
                sh 'docker run --rm -dp 3001:3000 --name app_dev nodedev:v1.0'
            }
        }
    }
}
