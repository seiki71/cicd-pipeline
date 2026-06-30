pipeline {
    agent any

    tools {
        nodejs 'node'
    }

    stages {
        stage('Linter') {
            steps {
                sh 'docker run --rm -i hadolint/hadolint < Dockerfile'
            }
        }
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
                sh 'docker build -t seiki71/nodemain:v1.0 .'
            }
        }
                stage('Scan Image') {
            steps {
                sh 'docker run aquasec/trivy image seiki71/nodemain:v1.0'
            }
        }
        stage('Docker Push') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker cred') {
                        sh 'docker push seiki71/nodemain:v1.0'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                build job: 'deploy_to_main'
            }
        }
    }
}