pipeline {
    agent any
    stages {
        stage('Build Application') {
            steps {
                sh 'mvn -f pom.xml clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifact"
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Test Application') {
            steps {
                echo 'Testing the Application'
            }
        }

        stage('Nexus Deploy') {
            steps {
                echo 'Deploying Artifact to Nexus'
            }
        }

        stage ('Deploy to Staging Enviornment') {
            steps {
                script {
                    deploy adapters: [tomcat9(credentialsId: 'tomcat-mgk', path: '', url: 'http://172.31.31.14:8080')], contextPath: '/', onFailure: false, war: '**/*.war'
                }
            }
        }


    }
}