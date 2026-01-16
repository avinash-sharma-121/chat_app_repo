pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/avinash-sharma-121/chat_app_repo.git'
            }
        }
        /*
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
        */

        stage('Generated tag for docker image') {
            steps {
                script {
                    env.IMAGE_TAG = sh (
                        script: "echo \$(git rev-parse --short HEAD)",
                        returnStdout: true
                    ).trim()
                    echo "Generated Image Tag: ${env.IMAGE_TAG}"
                }
            }
        }

        stage("docker build") {
            parallel {
                
                stage("build fronteend") {
                    steps{
                        script {
                            echo "Building Frontend Docker Image with tag: ${env.IMAGE_TAG}"
                            sh """
                            pwd
                            cd frontend
                            docker build -t avisharma82/chat_app_frontend:${env.IMAGE_TAG} .
                            """
                        }
                    }
                }
                
                
                stage("build backend") {
                    steps{
                        script {
                            echo "Building Backend Docker Image with tag: ${env.IMAGE_TAG}"
                            sh """
                            pwd
                            cd backend
                            docker build -t avisharma82/chat_app_backend:${env.IMAGE_TAG} .
                            """
                        }
                    }
                }
            }
        }

        stage('trivy scanner') {
            parallel {
                stage('frontend scanner'){
                    steps{
                        sh "echo Scanning Frontend Docker Image"
                    }
                }
                stage('backend scanner'){
                    steps{
                        sh "echo Scanning Backend Docker Image"
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

