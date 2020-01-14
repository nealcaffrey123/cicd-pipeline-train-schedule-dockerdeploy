pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            
             }
        }
         stage('Build docker image'){
             steps {
                sh 'docker build -t nlsaiteja/trainschedule:1.0 .'
             }
        }
         stage('Push Docker Image'){
             steps{
                sh 'docker push nlsaiteja/trainschedule:1.0'
             }
        }
         stage('Deploy'){
             steps{
                sh 'ssh cloud_user@52.226.90.27'
                sh 'sleep 10'
                sh 'docker pull nlsaiteja/trainschedule:1.0'
                sh 'docker run nlsaiteja/trainschedule:1.0'
             }
        }
           
    }
}
