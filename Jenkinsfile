pipeline {
    agent any

    stages {
        stage('LMS Code Analysis') {
            steps {
                echo 'Preparing Sonar Analysis'
                //sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://18.237.73.211:9000" -v ".:/usr/src" -e SONAR_TOKEN="sqp_d54b04dba6daef43a16855921c1bda41e062e9ef" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
                echo 'Completed Sonar Analysis'
            }
        }
        stage('LMS Build Artifacts') {
            steps {
                echo 'Preparing LMS Build'
                sh 'cd webapp && npm install && npm run build'
                echo 'Completed LMS Build'
            }
        }
        stage('LMS Release Artifacts') {
            steps {
                script {
                    echo 'Preparing LMS Release'
                    def packageJson = readJSON file: 'webapp/package.json'
                    def packageJSONVersion = packageJSON.version
                    echo "${packageJSONVersion}"
                    echo 'Completed LMS Release'
                }
            }
        }

        stage('LMS Deploy Artifacts') {
            steps {
                echo 'Preparing LMS Deployment'

                echo 'Completed LMS Deployment'
            }
        }

        stage('LMS Clean Up') {
            steps {
                echo 'Cleaning Up'
            }
        }
    }
}