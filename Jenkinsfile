pipeline {
    agent any
    stages {
        stage('Code Quality') {
            steps {
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://54.213.71.83:9000" -v ".:/usr/src" -e SONAR_TOKEN="sqa_4481f71bf5bbae6814a4943b03635810008d84cd" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
            }
        }
        stage('Build') {
            steps {
                sh 'cd webapp && npm install && npm run build'
            }
        }
        stage('Deploy') {
            steps {
                sh 'free -m'
            }
        }
    }
}