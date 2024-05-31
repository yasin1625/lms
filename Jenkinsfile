pipeline {
    agent any

    stages {
        stage('Sonar Analysis') {
            steps {
                echo 'CODE QUALITY CHECK'
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://34.214.127.143:9000" -e SONAR_LOGIN="sqp_31a2a065a5c706f2d31e4da19e61b346232ab619" -e SONAR_SCANNER_OPTS="\'-Dsonar.projectKey=lms\'"  -v ".:/usr/src" sonarsource/sonar-scanner-cli'
                echo 'CODE QUALITY COMPLETED'
            }
        }
        stage('Build LMS') {
            steps {
                echo 'Build LMS'
                sh 'cd webapp && npm install && npm run build'
                echo 'Build Completed'
            }
        }
        stage('Release LMS') {
            steps {
                script {
                    def packageJson = readJSON file: 'webapp/package.json'
                    def packageJSONVersion = packageJson.version
                    echo "${packageJSONVersion}"
                    sh "zip webapp/lms-${packageJSONVersion}.zip -r webapp/dist"
                    sh "curl -v -u admin:lms12345 --upload-file webapp/lms-${packageJSONVersion}.zip http://34.214.127.143:8081/repository/lms/"
                    sh "rm -rf webapp/node_modules webapp/dist"
                }
            }
        }

        stage('Deploy LMS') {
            steps {
                script {
                    def packageJson = readJSON file: 'webapp/package.json'
                    def packageJSONVersion = packageJson.version
                    echo "${packageJSONVersion}"
                    sh "curl -u admin:lms12345 -X GET \'http://34.214.127.143:8081/repository/lms/lms-${packageJSONVersion}.zip\' --output lms-'${packageJSONVersion}'.zip"
                    sh 'sudo rm -rf /var/www/html/*'
                    sh "sudo unzip -o lms-'${packageJSONVersion}'.zip"
                    sh "sudo cp -r webapp/dist/* /var/www/html"
                    sh "rm -rf webapp/dist"
                }
            }
        }

    }
}


