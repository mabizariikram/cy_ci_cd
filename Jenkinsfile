pipeline {
    agent any  // utilise l'agent Jenkins classique pour le checkout
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Run Cypress in Docker') {
            agent {
                docker {
                    image 'cypress/included:latest'
                    args '-u root --entrypoint='
                }
            }
            steps {
                sh 'npm ci'
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
