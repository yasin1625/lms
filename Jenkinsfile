pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'BUILDING'
                sh 'cat /etc/os-release'
            }
        }
        stage('Test') {
            steps {
                echo 'TESTING'
                sh 'free'
            }
        }
        stage('Deploy') {
            steps {
                echo 'DEPLOYING'
                sh 'df -h'
            }
        }
    }
}