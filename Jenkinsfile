pipeline {
    agent any

    stages {
        stage('Sonar Analysis') {
            steps {
                echo 'CODE QUALITY CHECK'
                sh 'cat /etc/os-release'
                sh 'sudo docker container ls'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
