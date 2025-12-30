pipeline {
    agent any
    stages {
        // Comment one-liner in Build stage
         /* stage('Build') {

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
        }  */
        stage('Test') {
            agent {
              docker {
                    image 'node:18-alpine'
                    args '-u root:root'
                    reuseNode true
                }
            }
            steps {
                sh '''
                   echo "Test stage"
                   echo "Test stage"
                   test -f build/index.html
                   npm test
                '''
            }
        }
        stage('E2E') {
            /*
             Build...
            */
            agent {
              docker {
                    image 'mcr.microsoft.com/playwright:v1.57.0-noble'
                    reuseNode true
                    args '-u root:root'
                }
            }
            steps {
                sh '''
                    npm install serve
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