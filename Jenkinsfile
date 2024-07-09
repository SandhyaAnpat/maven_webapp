pipeline {
    agent any
    environment {
        PATH = "$PATH:/usr/share/maven/bin"
    }
    stages {
        stage('Get Code') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/SandhyaAnpat/maven_webapp.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sshagent(credentials: ['tomcat-deploy']) {
                        sh "scp -o StrictHostKeyChecking=no target/hello.war ubuntu@54.83.115.85:/opt/tomcat/webapps"
                    }
                }
            }
        }
    }
}
