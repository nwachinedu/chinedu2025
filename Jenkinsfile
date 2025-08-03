pipeline {
    agent any

    stages {
        stage('build') {
            agents {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls-la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls-la
                '''
            }
        }
        stage('test') {
            agents {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            
            steps {
                sh '''
                test -f Jenkinsfile || echo "Jenkinsfile does not exist"
                npm test
                '''
            }
        }
    }
}