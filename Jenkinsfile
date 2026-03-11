pipeline {
    agent any

    stages {
        stage('Validate SQL File') {
            steps {
                sh 'test -f init.sql'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Security scan stage placeholder'
            }
        }

        stage('Container Build') {
            steps {
                sh 'docker build -t ecommerce-database:jenkins .'
            }
        }

        stage('Container Push') {
            steps {
                echo 'Container push stage placeholder'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy stage placeholder'
            }
        }
    }
}
