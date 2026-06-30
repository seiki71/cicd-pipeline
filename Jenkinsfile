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
                sh 'docker build -t seiki71/nodedev:v1.0 .'
            }
        }
        stage('Push Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker cred') {
                        sh 'docker push seiki71/nodedev:v1.0'
                    }
                }
            }
        }
        stage('Deploy') {
            build job: 'Deploy_to_dev'
        }
    }
}
