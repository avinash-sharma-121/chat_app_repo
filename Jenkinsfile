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
/*
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
                        sh "trivy image --severity HIGH,CRITICAL avisharma82/chat_app_frontend:${env.IMAGE_TAG}"
                    }
                }
                stage('backend scanner'){
                    steps{
                        sh "echo Scanning Backend Docker Image"
                        sh "trivy image --severity HIGH,CRITICAL avisharma82/chat_app_backend:${env.IMAGE_TAG}"
                    }
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    sh """
                        echo "Pushing Frontend Docker Image to Docker Hub"
                        docker push avisharma82/chat_app_frontend:${env.IMAGE_TAG}
                        
                        echo "Pushing Backend Docker Image to Docker Hub"
                        docker push avisharma82/chat_app_backend:${env.IMAGE_TAG}
                    """
                }
            }
        }
*/
/*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 */


        stage('update k8s deployment file') {
            steps {
                script {
                    sh '''
                        #cd helm_chat_app/
                        sed -i 's|tag: .*|tag: "'${IMAGE_TAG}'"|g' helm_chat_app/values.yaml

                        #sed -i 's|avinashsharma82/chat_app_frontend:.*|avinashsharma82/chat_app_frontend:'${IMAGE_TAG}'|g' values.yaml
                        #sed -i 's|avinashsharma82/chat_app_backend:.*|avinashsharma82/chat_app_backend:'${IMAGE_TAG}'|g' values.yaml
                    '''
                }
            }

        }

        stage('git push tag') {
            steps {
                script {
                 withCredentials([gitUsernamePassword(credentialsId: 'github_cre', gitToolName: 'Default')]) {
                    sh '''
                        # Configure user info for the commit
                        git config user.name "avinash-sharma-121"
                        git config user.email "kumaravinashsharma81@gmail.com"
                        # Create and push the tag
                        #git tag -a v${IMAGE_TAG} -m "Tagging version v${IMAGE_TAG}"
                        git add .
                        git commit -m "Automated commit from Jenkins"

                        # Push changes using the bound credentials
                        git push https://github.com/avinash-sharma-121/chat_app_repo.git HEAD:main
                    '''
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

