pipeline {
    agent any
    environment{
        NETLIFY_SITE_ID = '4f347bfb-604a-48d0-bb36-61e858cd5889'
        NETLIFY_AUTH_TOKEN = credentials('netli')
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
                    npm install netlify-cli -g
                    node_modules/.bin/netlify --version  
                    echo "Site ID is $NETLIFY_SITE_ID"
                    node_modules/.bin/netlify status     
                    node_modules/.bin/netlify deploy --dir=build --prod            

                '''
            }
        }   
    }
}
