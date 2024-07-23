pipeline {
    agent any

    stages {
        stage('Code Quality') {
            steps {
                sh 'sleep 5' 
                echo 'Sonar Analysis Completed'
            }
        }
        
        stage('Build LMS') {
            steps {
                sh 'sleep 10' 
                echo 'LMS Build Completed'
            }
        }
        
        stage('Publish LMS') {
            steps {
                sh 'sleep 10' 
                echo 'Upload Artifacts To NEXUS'
            }
        }
        
        stage('Deploy LMS') {
            steps {
                sh 'sleep 10' 
                echo 'LMS App Deployed'
            }
        }
    }
}
