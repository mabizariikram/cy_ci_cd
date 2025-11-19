pipeline {
    agent {
        docker {
            image 'cypress/included:latest'
            args '-u root --entrypoint=""'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                // Supprimer le dossier repo s'il existe déjà
                sh 'rm -rf repo'

                // Cloner le dépôt
                sh 'git clone https://github.com/mabizariikram/cy_ci_cd.git repo'

                // Entrer dans le dossier repo
                dir('repo') {
                    // Installer les dépendances
                    sh 'npm install'
                    sh 'npm install --save-dev @cypress/grep'

                    // Lancer le test Cypress spécifique
                    sh 'npx cypress run --spec="cypress/e2e/login.cy.js"'
                }
            }
        }
    }
    post {
        always {
            // Archiver les résultats
            archiveArtifacts artifacts: 'repo/results/*.*', fingerprint: true
            junit 'repo/results/*.xml'
        }
    }
}
