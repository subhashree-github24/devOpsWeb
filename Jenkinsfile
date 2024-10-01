pipeline{
    agent any

    tools {
        maven 'localMaven'
    }
    stages{
        stage('Build java Application'){
            steps {
                 sh 'mvn clean package'

            }
            post {
                success{
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts:'**/target/*.war'
                }
            }
        }
        stage('Deployment to staging server'){
            parallel{
                stage('Deploy to Tomcat Server1'){
                    steps{deploy adapters: [tomcat9(credentialsId: 'tomcat-b15', path: '', url: 'http://13.201.41.60:8080/')], contextPath: null, war: '**/*.war'

                    }
                }
            }
        }
    }
}
