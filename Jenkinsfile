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

        stage('Prepare Environment') {
            steps {
                sh '''
                mkdir -p /home/projects
                '''
            }
        }

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
                ls
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
