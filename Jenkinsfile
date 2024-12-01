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
                    ls -a
                    npm ci 
                    npm run build
                    ls -a
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
                    ls -a
                    ls build/
                    test -f buid/index.html
                    npm test
                '''
            }
        }
    }
}
