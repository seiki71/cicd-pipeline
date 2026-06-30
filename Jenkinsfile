pipeline {
    agent any

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
                sh 'docker build -t nodemain:v1.0 .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker stop app_main || true '
                sh 'docker run --rm -dp 3000:3000 --name app_main nodemain:v1.0'
            }
        }
    }
}