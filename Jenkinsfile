pipeline {
    agent any

    environment {
        NEXUS_URL = 'http://localhost:9090/repository/front-end-repo/'
        NEXUS_CREDENTIALS_ID = 'nexus-credentials-id'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Checkout the latest code from GitHub
                    checkout scm

                    // Install dependencies and build the front-end application
                    sh 'yarn install'    // or 'yarn install' if you're using Yarn
                    sh 'yarn run build'  // or 'yarn build' if you're using Yarn
                }
            }
        }
        stage('Deploy to Nexus') {
            steps {
                script {
                    // Archive build artifacts
                    archiveArtifacts artifacts: 'dist/**', allowEmptyArchive: true

                    // Upload build artifacts to Nexus
                    nexusArtifactUploader(
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        nexusUrl: "${env.NEXUS_URL}",
                        groupId: 'your-group-id',
                        version: '1.0.0',
                        repository: 'front-end-repo',
                        credentialsId: "${env.NEXUS_CREDENTIALS_ID}",
                        artifacts: [
                            [artifactId: 'front-end-app', classifier: '', file: 'dist/your-app.zip', type: 'zip']
                        ]
                    )
                }
            }
        }
    }
}
