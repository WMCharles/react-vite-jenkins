pipeline {
    agent {
        docker {
            image 'node:20-alpine'
            args '-u root -v /home/projects:/home/projects'
        }
    }
    environment {
        HOME = '/var/www/html'
    }
    stages {

        stage('Build') {
            steps {
                echo 'Building..'
                sh '''
                rm -rf dist
                rm -rf node_modules
                npm install
                npm run build
                echo "task complete"
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }

        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "doing delivery stuff.."
                '''
            }
        }
    }

    post {
        always {
            script {
                sh '''
                cp -r ${WORKSPACE}/. /var/www/html/react_jenkins
                cd /var/www/html/react_jenkins
                ls
                '''
            }
        }
    }
}
