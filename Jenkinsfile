pipeline{
    agent {
        label 'javabuild'
    }

    tools {
        maven 'localmaven'
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
                    steps{
                        deploy adapters: [tomcat9(credentialsId: 'tomcat-b15', path: '', url: 'http://3.109.155.163:8080/')], contextPath: null, war: '**/*.war'
                    }
                }
            }
        }
    }
}
