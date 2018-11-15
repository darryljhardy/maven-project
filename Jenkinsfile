pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        stage('Deploy to Tomcat 01'){
            steps {
                build job: 'deploy-to-tomcat-01'
            }
        }
    }
}
