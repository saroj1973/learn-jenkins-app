pipeline {
    agent any
    environment{
        NETLIFY_SITE_ID = '731c4759-9b16-44f6-83b2-4eada589b86a'
    }
    stages {
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
        stage('Deploy') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm install netlify-cli
                    node_modules/.bin/netlify --version  
                    node_modules/.bin/netlify status     
                    echo "Site ID is $NETLIFY_SITE_ID"
                '''
            }
        }
        

    }
}
