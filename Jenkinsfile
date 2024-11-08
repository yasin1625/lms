pipeline {
    agent any

    stages {
        stage('Code Analysis') {
            steps {
                echo 'Started Code Analysis'
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://18.237.107.186:9000" -v ".:/usr/src" -e SONAR_TOKEN="sqp_c319bfe321de6eb1a007b6acf3e2032f8713e369" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
                echo 'Code Analysis Completed'
            }
        }
        stage('Build Artifact') {
            steps {
                echo 'Started Buidling Artifact'
                sh 'cd webapp && npm install && npm run build'
                echo 'Buidling Artifact Completed'
            }
        }
        stage('Publish LMS Artifact') {
           steps {
               script {
                   def packageJson = readJSON file: 'webapp/package.json'
                   def packageJSONVersion = packageJson.version
                   echo "${packageJSONVersion}"
                   sh "zip webapp/lms-${packageJSONVersion}.zip -r webapp/dist"
                   sh "curl -v -u admin:lms12345 --upload-file webapp/lms-${packageJSONVersion}.zip http://18.237.107.186:8081/repository/lms/"
               }
           }
       }
       stage('Deploy LMS') {
           steps {
               script {
                   def packageJson = readJSON file: 'webapp/package.json'
                   def packageJSONVersion = packageJson.version
                   echo "${packageJSONVersion}"
                   sh "curl -u admin:lms12345 -X GET \'http://18.237.107.186:8081/repository/lms/lms-${packageJSONVersion}.zip\' --output lms-'${packageJSONVersion}'.zip"
                   sh 'sudo rm -rf /var/www/html/*'
                   sh "sudo unzip -o lms-'${packageJSONVersion}'.zip"
                   sh "sudo cp -r webapp/dist/* /var/www/html"
               }
           }
       }
       stage('Clean Up Workspace') {
           steps {
                   echo 'Cleaning Work Space'
                   // Install Cleanup Workspace plugin to make below command work
                   cleanWs()
           }
       }
    }
}
