pipeline {
    agent any

    environment {
        IMAGE_NAME = "mukuld86/medilearn-ai"
        TAG = "latest"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/mukuld86/MediLearn-AI.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Next.js App') {
            steps {
                withCredentials([
                    string(credentialsId: 'mongodb_uri', variable: 'MONGODB_URI'),
                    string(credentialsId: 'jwt_secret', variable: 'AUTH_JWT_SECRET'),
                    string(credentialsId: 'gemini_key', variable: 'GEMINI_API_KEY')
                ]) {
                    sh '''
                    export MONGODB_URI=$MONGODB_URI
                    export AUTH_JWT_SECRET=$AUTH_JWT_SECRET
                    export GEMINI_API_KEY=$GEMINI_API_KEY

                    npm run build
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                withCredentials([
                    string(credentialsId: 'mongodb_uri', variable: 'MONGODB_URI'),
                    string(credentialsId: 'jwt_secret', variable: 'AUTH_JWT_SECRET'),
                    string(credentialsId: 'gemini_key', variable: 'GEMINI_API_KEY')
                ]) {
                    sh '''
                    docker build \
                    --build-arg MONGODB_URI=$MONGODB_URI \
                    --build-arg AUTH_JWT_SECRET=$AUTH_JWT_SECRET \
                    --build-arg GEMINI_API_KEY=$GEMINI_API_KEY \
                    -t $IMAGE_NAME:$TAG .
                    '''
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    sh '''
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    docker push $IMAGE_NAME:$TAG
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'CI Pipeline completed successfully!'
        }

        failure {
            echo 'CI Pipeline failed!'
        }
    }
}