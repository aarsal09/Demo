pipeline{
    agent any tools{
        maven 'maven3'
    }
    stages{
        stage('Build')
        {
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo"Archiving the Artifacts"
                    archieveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage{
            'Deploy to tomcat server'{
                steps{
                    deploy adapters: [tomcat9(credentialsId: 'bad59bd4-52c5-453b-998a-3a48479bc047', path: '', url: 'http://localhost:7080/')], contextPath: null, war: '**/*.war'
                }
            }
        }
    }
}
