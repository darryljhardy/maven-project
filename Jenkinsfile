pipeline {
    agent any
    environment {
        MY_BAT_DOCKER='C:\\Program Files\\Docker Toolbox\\docker'
        MY_SH_DOCKER='/c/Program Files/Docker Toolbox/docker'
    }
    stages{
        stage('Build'){
            steps {
                echo "Executing Maven Clean Package"
                sh "mvn clean package"
                //bat "${MY_BAT_DOCKER} . -t tomcatwebapp:${env.BUILD_ID}"
                sh "${MY_SH_DOCKER} . -t tomcatwebapp:${env.BUILD_ID}"
                //sh "export"
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
