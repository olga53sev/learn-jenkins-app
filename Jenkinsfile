pipeline {
        agent {
              docker {
                    image 'node:18-alpine'
                    args '-u root:root'
                    reuseNode true
                }
        }


    stages {
        // Comment one-liner in Build stage
        stage('Build') {

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
        stage('Test') {
            /*
             Comment block in test stage line 1
             Comment block in test stage line2
            */
            steps {
                sh '''
                   echo "Test stage"
                   test -f build/index.html
                   npm test
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