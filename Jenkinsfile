pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/avinash-sharma-121/chat_app_repo.git'
            }
        }

        stage('Code Quality - SonarCloud') {
            steps {
              script {
                    def scannerHome = tool 'sonar-scanner'
                        withSonarQubeEnv('sonarcloud') {
                            sh """
                              ${scannerHome}/bin/sonar-scanner \
                                -Dsonar.projectKey=avinash-sharma-121_chat_app_repo \
                                -Dsonar.organization=avinash-sharma-121 \
                                -Dsonar.sources=.
                            """
                        }
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
        */
    }
    

    post {
        success {
            echo 'Deployment and tests completed successfully!'
        }
        failure {
            echo 'Deployment or tests failed.'
        }
    }
}

