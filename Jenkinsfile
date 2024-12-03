pipeline {
    agent any

    stages {
        stage('Code Quality') {
            steps {
                echo 'Sonar Analysis'
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://172.212.225.128:9000" -v ".:/usr/src" -e SONAR_TOKEN="sqp_87e32cf857353ace0e9c31221e2a94c202dff736" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
            }
        }
    }
}