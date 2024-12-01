pipeline {
    agent any

    stages {
        stage("build"){
            agent {
                docker {
                    image "node:18-alpine"
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm ci 
                    npm run build
                '''
            }
        }

        stage("Test"){

            agent {
                docker {
                    image "node:18-alpine"
                    reuseNode true
                }
            }

            steps {

                sh '''
                    test -f buid/index.html
                    npm test
                '''
            }
        }
    }
}
