pipeline {
    agent {
        docker {
            image 'mcr.microsoft.com/playwright:v1.63.0-noble'
            args '--ipc=host'          // antes: '--ipc=host -u pwuser'
            reuseNode true
        }
    }

    triggers {
        cron('*/30 * * * *')
    }

    options {
        disableConcurrentBuilds()
        buildDiscarder(logRotator(numToKeepStr: '20', artifactNumToKeepStr: '10'))
    }

    stages {
        stage('Instalar dependencias') {
            steps { sh 'npm ci' }
        }
        stage('Tests') {
            steps { sh 'npx playwright test --project=Computadora' }
        }
    }

    post {
        always {
            junit 'results.xml'
            archiveArtifacts 'playwright-report/**, test-results/**'
            publishHTML(target: [
                allowMissing: true,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'playwright-report',
                reportFiles: 'index.html',
                reportName: 'Playwright Report'
            ])
        }
    }
}
