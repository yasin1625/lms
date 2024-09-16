pipeline {
    agent any
    stages {
        stage('Sonar Analysis') {
            steps {
                echo 'CODE QUALITY CHECK'
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://52.11.92.224:9000" -v ".:/usr/src" -e SONAR_TOKEN="sqp_683194bc8b08654f00afc1f741cbba7e74a49ede" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
                echo 'CODE QUALITY COMPLETED' 
            }
        }
        stage('Test') {
            steps {
                echo 'TESTING'
                sh 'free -m'
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