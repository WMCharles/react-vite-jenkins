pipeline {
    agent {
        docker {
            image 'node:20-alpine'
            args '-u root'
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
                sh '''
                pwd
                cd /home/projects
                pwd
                rm -rf /home/projects/react
                cp -r ${WORKSPACE}/dist ./
                touch /home/projects/wafula.txt
                '''
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
}
