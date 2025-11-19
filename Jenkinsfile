pipeline {
    agent {
        docker {
            image 'cypress/included:latest'
            args '-u root'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                sh 'git clone https://github.com/mabizariikram/cy_ci_cd.git repo'
                dir('repo') {
                    sh 'npm ci'
                    sh 'npx cypress run --spec="cypress/e2e/login.cy.js"'
                }
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'repo/results/*.*', fingerprint: true
            junit 'repo/results/*.xml'
        }
    }
}
