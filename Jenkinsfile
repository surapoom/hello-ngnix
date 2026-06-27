pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'docker build -t hello-nginx:${BRANCH_NAME} .'
            }
        }

        stage('Deploy') {
            steps {
                script {

                    if (env.BRANCH_NAME == "main") {

                        sh '''
                        docker rm -f hello-main || true

                        docker run -d \
                          --name hello-main \
                          -p 8007:80 \
                          hello-nginx:main
                        '''

                    } else if (env.BRANCH_NAME == "dev") {

                        sh '''
                        docker rm -f hello-dev || true

                        docker run -d \
                          --name hello-dev \
                          -p 8008:80 \
                          hello-nginx:dev
                        '''

                    }

                }
            }
        }

    }
}