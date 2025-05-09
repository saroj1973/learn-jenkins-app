pipeline {
    agent any
    environment{
        NETLIFY_SITE_ID = '4f347bfb-604a-48d0-bb36-61e858cd5889'
    }
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
        
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
    }
}
