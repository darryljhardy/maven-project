pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                echo "Executing Maven Clean Package"
                sh "mvn clean package"
                sh "export"
                sh "docker build . -t tomcatwebapp:${env.BUILD_ID}"
            }
            post {
                success {
                    echo "Now Archiving..."
                    archiveArtifacts artifacts: "**/target/*.war"
                }
            }
        }
    }
 
}
