pipeline {
    agent {
        docker {
            image 'mcr.microsoft.com/playwright:v1.63.0-noble'
            args '--ipc=host -u pwuser'
            reuseNode true
        }
    }
    stages {
        stage('Instalar dependencias') {
            steps { sh 'npm ci' }
        }
        stage('Tests') {
            steps { sh 'npx playwright test --project=Computadora' }
        }
    }
}
