pipeline {
    agent {
        node {
            label 'docker-host'
        }
    }
    stages {
        stage('build') {
            steps {
                checkout  scm
                sh 'docker-compose build'
                sh 'docker-compose up -d'
            }
        }

        stage('tests') {
            steps {
                sh 'python2.7 app.py'
            }
        }
    }
    post {
        always {
            sh "docker-compose down"
            deleteDir()
        }
        success {
            echo 'Test Successful'
        }

        failure {
            echo 'Test failed'
        }
    }
}