pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                credentialsId: '7f7f77eb-d01b-4d86-b22d-cdef8b45ff84',
                url: 'https://github.com/rakshith31-hub/MyMavenAnsibleVVP.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                sh 'ansible-playbook playbook.yml -i hosts.ini'
            }
        }
    }

    post {
        success {
            echo 'Build and Deployment Successful!'
        }

        failure {
            echo 'Pipeline Failed!'
        }
    }
}
