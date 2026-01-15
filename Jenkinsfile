pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/avinash-sharma-121/chat_app_repo.git'
            }
        }

        stage('code smell check') {
            steps {
                script {
                    sh 'echo "testing with sonarQube"'
                    sh """
                        sonar-scanner \
                        -Dsonar.projectKey=chat_app_repo \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=https://sonarcloud.io \
                        -Dsonar.login=56d5f434209e6470ff604d380ad9dbb4cb88efc7
                    """
                }
            }
        }

/*
        stage('Test') {
            steps {
                script {
                    sh '''
                        sleep 15
                        curl -f http://localhost:5001/health
                        curl -f http://localhost/ || exit 1
                    '''
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh 'docker-compose up -d --build'
                }
            }
        }
    }
    */

    post {
        success {
            echo 'Deployment and tests completed successfully!'
        }
        failure {
            echo 'Deployment or tests failed.'
        }
    }
}

}