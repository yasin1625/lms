pipeline {
    agent any

    stages {
        stage('Sonar Analysis') {
            steps {
                echo 'CODE QUALITY CHECK'
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://54.190.152.188:9000" -e SONAR_LOGIN="sqp_7f6ed372254a6a1ac8a1f5657dd74f46621af166"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
                echo 'CODE QUALITY DONE'
            }
        }
        stage('Build LMS') {
            steps {
                echo 'BUILD LMS APP'
                sh 'cd webapp && npm install && npm run build'
                echo 'BUILD COMPLETED'
            }
        }
        stage('Release LMS') {
            steps {
                script {
                    echo "RELEASE LMS Artifacts"       
                    def packageJSON = readJSON file: 'webapp/package.json'
                    def packageJSONVersion = packageJSON.version
                    sh "zip webapp/lms-${packageJSONVersion}.zip -r webapp/dist"
                    sh "curl -v -u admin:lms12345 --upload-file webapp/lms-${packageJSONVersion}.zip http://54.190.152.188:8081/repository/lms/"     
            }
            }
        }
    }
}
