pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                echo 'Executing Maven Clean Package'
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to Dev'){
            steps {
                build job: 'deploy-to-dev'
            }
            post {
                success {
                    echo 'Code successfully deployed to Dev.'
                }
                failure {
                    echo 'Oh oh. Deployment to Dev failed!'
                }
            }
        }
        stage('Deploy to QA'){
            steps {
                build job: 'deploy-to-qa'
            }
            post {
                success {
                    echo 'Code successfully deployed to QA.'
                }
                failure {
                    echo 'Oh oh. Deployment to QA failed!'
                }
            }
        }
        stage('Deploy to PT'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve PT Deployment?'
                }
                build job: 'deploy-to-pt'
            }
            post {
                success {
                    echo 'Code successfully deployed to PT.'
                }
                failure {
                    echo 'Oh oh. Deployment to PT failed!'
                }
            }
        }
        stage('Deploy to Prod'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve Production Deployment?'
                }
                build job: 'deploy-to-prod'
            }
            post {
                success {
                    echo 'Code successfully deployed to Production.'
                }
                failure {
                    echo 'Oh oh. Deployment to Production failed!'
                }
            }
        }
    }
}
