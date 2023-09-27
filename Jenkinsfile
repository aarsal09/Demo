pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to Tomcat server') { // Corrected the stage name
            steps {
                script {
                    def server = [
                        tomcat9(
                            credentialsId: 'bad59bd4-52c5-453b-998a-3a48479bc047',
                            path: '',
                            url: 'http://localhost:7080/'
                        )
                    ]
                    deploy adapters: server, contextPath: '', war: '**/*.war'
                }
            }
        }
    }
}
