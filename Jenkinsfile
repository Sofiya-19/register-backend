pipeline {
    agent any

    tools {
        nodejs 'NodeJS'  // Ensure NodeJS is installed and configured
    }
    
    environment {
        NODEJS_HOME = '/Users/sofiyabalamurugan/.nvm/versions/node/v20.18.1/bin/node'
        PATH = "$NODEJS_HOME:$PATH:/Users/sofiyabalamurugan/Downloads/sonar-scanner-6.2.1.4610-macosx-aarch64/bin"
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
                SONAR_TOKEN = credentials('sonarqube-token')  
            }
            steps {
                // Invoke sonar-scanner directly (path included in PATH environment variable)
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
