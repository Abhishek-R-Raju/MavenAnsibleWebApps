pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Abhishek-R-Raju/MavenAnsibleWebApps.git'
            }
        }

        stage('Build') {
            steps {
                dir('MavenAnsibleWebApp') {
                    sh 'mvn clean package'
                }
            }
        }

        stage('Archive WAR') {
            steps {
                dir('MavenAnsibleWebApp') {
                    archiveArtifacts artifacts: 'target/MavenWebAppJenkinsIntegrationusingAnsible.war', fingerprint: true
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                dir('MavenAnsibleWebApp') {
                    sh 'ansible-playbook ansible/playbook.yml -i ansible/hosts.ini'
                }
            }
        }
    }
}


