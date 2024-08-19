pipeline {
    agent any
    stages {
        stage('Code Quality') {
            steps {
                echo 'Sonar Analysis Started'
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://172.212.98.180:9000" -v ".:/usr/src" -e SONAR_TOKEN="sqp_02ef59ecebb19f94bc01ed4bf853b68f29a8c4fc" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms' 
                echo 'Sonar Analysis Completed'
            }
        }
        
        stage('Build LMS') {
            steps {
                echo 'LMS Build Started'
                sh 'cd webapp && npm install && npm run build' 
                echo 'LMS Build Completed'
            }
        }
        
        stage('Release LMS') {
            steps {
                script {
                    def packageJson = readJSON file: 'webapp/package.json'
                    def packageJSONVersion = packageJson.version
                    echo "${packageJSONVersion}"
                    sh "zip webapp/lms-${packageJSONVersion}.zip -r webapp/dist"
                    sh "curl -v -u admin:lms12345 --upload-file webapp/lms-${packageJSONVersion}.zip http://172.212.98.180:8081/repository/lms/"
                }
            }
        }

        stage('Deploy LMS') {
            steps {
                script {
                    def packageJson = readJSON file: 'webapp/package.json'
                    def packageJSONVersion = packageJson.version
                    echo "${packageJSONVersion}"
                    sh "curl -u admin:lms12345 -X GET \'http://172.212.98.180:8081/repository/lms/lms-${packageJSONVersion}.zip\' --output lms-'${packageJSONVersion}'.zip"
                    sh 'sudo rm -rf /var/www/html/*'
                    sh "sudo unzip -o lms-'${packageJSONVersion}'.zip"
                    sh "sudo cp -r webapp/dist/* /var/www/html"
                }
            }
        }

        stage('CleanUp LMS') {
            steps {
                    echo 'Cleaning Work Space'
                    // Install Cleanup Workspace plugin to make below command work
                    cleanWs()
            }
        }

    }
}