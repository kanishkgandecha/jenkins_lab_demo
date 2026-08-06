pipeline {
    agent any

    environment {
        PATH = "/opt/homebrew/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    }

    stages {

        stage('Verify Node') {
            steps {
                sh '''
                    echo "Node Version:"
                    node -v

                    echo "NPM Version:"
                    npm -v
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'CI=true npm test -- --watchAll=false'
            }
        }
    }

    post {
        success {
            echo 'Build Successful!'
        }

        failure {
            echo 'Build Failed!'
        }

        always {
            cleanWs()
        }
    }
}