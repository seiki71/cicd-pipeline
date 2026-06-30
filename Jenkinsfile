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
                sh 'docker build -t nodemain:v1.0 .'
            }
        }
        stage('Docker Push') {
            steps {
                sh "docker push seiki71/nodemain:v1.0"
            }
        }
        stage('Deploy') {
            steps {
                build job: 'deploy_to_main'
            }
        }
    }
}