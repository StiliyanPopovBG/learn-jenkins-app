pipeline {
    agent any

    stages {
        // This is a comment on paticular line
        /* block of codes
        line 1
        line 2
        
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
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh'''
                echo 'Test stage ...'
                # test -f build/index.html this is a comment in sh line
                npm test
                '''
            }
        }

        stage('E2E') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.49.0-noble'
                    reuseNode true
                }
            }
            steps {
                sh'''
                    npm install -g serve
                    node_modules/.bin/serve -s build
                    npx playwright test
                '''
            }
        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}