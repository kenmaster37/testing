pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Ver lo que bajó') {
            steps {
                sh 'ls -la'
                sh 'git log --oneline -3'
            }
        }
    }
}
