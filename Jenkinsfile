pipeline {
    agent {
        docker {
            image 'cypress/included:latest'
            args '-u=root --entrypoint='
        }
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install Cypress') {
            steps {
                sh 'npm ci'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npx cypress run --spec="cypress/e2e/login.cy.js"'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'results/*.*', fingerprint: true
            junit 'results/*.xml'
        }
    }
}
