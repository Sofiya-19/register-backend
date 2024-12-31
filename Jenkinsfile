pipeline {
    agent any

    tools {
        nodejs 'NodeJS'  // Ensure NodeJS tool configuration is available in Jenkins
    }
    
    environment {
        NODEJS_HOME = '/Users/sofiyabalamurugan/.nvm/versions/node/v20.18.1/bin/node'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Install and Build') {
            steps {
                sh '''
                npm install
                '''
            }
        }

        stage('SonarCodeAnalysis') {
            environment {
                SONAR_TOKEN = credentials('sonarqube-token')  // Ensure this credential is set in Jenkins
            }
            steps {
                sh '''
                sonar-scanner \
                    -Dsonar.projectKey=mern-backend \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=http://localhost:9000 \
                    -Dsonar.token=$SONAR_TOKEN
                '''
            }
        }
    }

    post {
        success {
            echo "Pipeline SUCCESSFULLY Build"
        }
        failure {
            echo "Pipeline failed"
        }
    }
}
