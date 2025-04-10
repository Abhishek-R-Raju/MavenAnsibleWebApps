pipeline {
    agent any  // Use any available Jenkins agent

    environment {
        LANG = 'en_US.UTF-8'
        LC_ALL = 'en_US.UTF-8'
    }

    tools {
        maven 'Maven'  // This should match the Maven installation name configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Abhishek-R-Raju/MavenAnsibleWebApps.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the Maven Web Application...'
                sh 'mvn clean package'
            }
        }

        stage('Archive') {
            steps {
                echo 'Archiving the WAR file...'
                archiveArtifacts artifacts: 'target/ MavenWebAppJenkinsIntegrationusingAnsible.war', fingerprint: true
            }
        }

        stage('Deploy to Tomcat using Ansible') {
            steps {
                echo 'Deploying the WAR file using Ansible...'
                // If needed, build again before deployment (optional)
                // sh 'mvn clean package'
                sh 'ansible-playbook ansible/playbook.yml -i ansible/hosts.ini'
            }
        }
    }

    post {
        success {
            echo 'Build and deployment completed successfully!'
        }
        failure {
            echo 'Build or deployment failed. Please check the logs.'
        }
    }
}

