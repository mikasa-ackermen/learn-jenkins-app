pipeline {
    agent any

    // options {
    //     skipDefaultCheckout() // Disables automatic SCM checkout
    // }

    stages {

        // stage('Prepare Workspace') {
        //     steps {
        //         cleanWs() // Cleans the workspace first
        //         checkout scm // Manually performs checkout
        //     }
        // }

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
                    test -f build/index.html
                    npm test
                '''
            }
        }
    }

    post {
        always { 
            
            junit "test-results/junit.xml"
        }
    }
}
