pipeline {
    agent any
    
    environment {
        // Ensure Maven is installed and named correctly
        MAVEN_HOME = tool 'Maven 3.8.6'
        // Nexus credentials ID configured in Jenkins credentials
        NEXUS_CREDENTIALS_ID = 'nexus-credentials-id'
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                script {
                    // Run Maven build
                    withMaven(maven: MAVEN_HOME) {
                        sh 'mvn clean install'
                    }
                }
            }
        }
        
        stage('Test') {
            steps {
                echo 'Testing the application...'
                script {
                    // Run Maven tests
                    withMaven(maven: MAVEN_HOME) {
                        sh 'mvn test'
                    }
                }
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                script {
                    // Deploy to Nexus
                    withMaven(maven: MAVEN_HOME) {
                        sh 'mvn deploy -DskipTests'
                    }
                }
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
