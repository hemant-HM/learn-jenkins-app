pipeline {
    agent any
    stages {
        
        /*
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        */
        stage('Test') {
            steps {
                sh '''
                    test -f public/index.html
                '''
                    // npm test
            }
        }
        stage('E2E') {
            agent {
                docker {
                    // image 'mcr.m icrosoft.com/playwright:v1.58.2-noble'
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    node_modules/.bin/serve -s build &
                    sleep 10
                    npx playwright test
                '''
                // npm install serve
                // & for background running
            }
        }
    }
    post {
        always {
            junit 'jest-results/junit.xml'
        }
    }
}
