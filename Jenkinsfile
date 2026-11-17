pipeline {
    agent { label 'ci-python-docker' }

    stages {
        stage('Prepare') {
            steps {
                sh 'mkdir -p dist'
                echo 'Ambiente preparado'
            }
        }

        stage('Build') {
            steps {
                sh '''
                    set -eu
                    printf 'Estado: OK\n' > dist/resultado.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh "grep -q 'Estado: OK' dist/resultado.txt"
            }
        }

        stage('Package') {
            steps {
                archiveArtifacts artifacts: 'dist/resultado.txt',
                                 fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Pipeline concluída'
        }

        failure {
            echo 'Pipeline com erro'
        }
    }
}