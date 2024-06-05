pipeline {
    agent any

    stages {
        stage('LMS Code Analysis') {
            steps {
                echo 'Preparing Sonar Analysis'

                echo 'Completed Sonar Analysis'
            }
        }
        stage('LMS Build Artifacts') {
            steps {
                echo 'Preparing LMS Build'

                echo 'Completed LMS Build'
            }
        }
        stage('LMS Release Artifacts') {
            steps {
                echo 'Preparing LMS Release'

                echo 'Completed LMS Release'
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