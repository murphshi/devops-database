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
                echo 'Static analysis placeholder for database'
            }
        }

        stage('Container Build') {
            steps {
                script {
                    def imageTag = "build-${env.BUILD_NUMBER}"
                    sh "docker build -t ecommerce-database:${imageTag} ."
                }
            }
        }

        stage('Build Environment Validation') {
            when {
                not {
                    anyOf {
                        branch 'develop'
                        branch 'main'
                        branch pattern: "release/.*", comparator: "REGEXP"
                    }
                }
            }
            steps {
                echo 'Build pipeline executed for feature branch or pull request validation'
            }
        }

        stage('Deploy to Dev') {
            when {
                branch 'develop'
            }
            steps {
                echo 'Deploying database to dev environment'
            }
        }

        stage('Deploy to Staging') {
            when {
                branch pattern: "release/.*", comparator: "REGEXP"
            }
            steps {
                echo 'Deploying database to staging environment'
            }
        }

        stage('Prod Approval') {
            when {
                branch 'main'
            }
            steps {
                input message: 'Approve deployment to production?', ok: 'Deploy'
            }
        }

        stage('Deploy to Prod') {
            when {
                branch 'main'
            }
            steps {
                echo 'Deploying database to production environment'
            }
        }
    }
}
