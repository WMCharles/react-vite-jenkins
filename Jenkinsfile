pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/WMCharles/react-vite-jenkins.git'
        BRANCH = 'main'
        NODE_VERSION = '20'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: "${BRANCH}", url: "${REPO_URL}"
            }
        }
        
        stage('Install Dependencies') {
            steps {
                script {
                    // Ensure Node.js is installed
                    def nodeExists = sh(script: 'node --version', returnStatus: true) == 0
                    if (!nodeExists) {
                        // Install Node.js using nvm
                        sh 'curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash'
                        sh '. ~/.nvm/nvm.sh && nvm install ${NODE_VERSION} && nvm use ${NODE_VERSION}'
                    }
                    // Install dependencies
                    sh '. ~/.nvm/nvm.sh && npm install'
                }
            }
        }
        
        stage('Build') {
            steps {
                script {
                    sh '. ~/.nvm/nvm.sh && npm run build'
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'build/**/*', allowEmptyArchive: false
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
