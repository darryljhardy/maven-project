pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                echo "Executing Maven Clean Package"
                sh "mvn clean package"
                sh "/c/Program Files/Docker Toolbox/docker build . -t tomcatwebapp:${env.BUILD_ID}"
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
