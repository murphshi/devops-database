pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'test -f init.sql'
                echo 'Database build validation completed'
            }
        }

        stage('Test') {
            steps {
                sh "grep -q 'CREATE TABLE' init.sql"
                echo 'Database test validation completed'
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
                    env.IMAGE_TAG = "build-${env.BUILD_NUMBER}"
                    sh "docker build -t ecommerce-database:${env.IMAGE_TAG} ."
                }
            }
        }

        stage('Container Push') {
            steps {
                echo "Container push placeholder for ecommerce-database:${env.IMAGE_TAG}"
            }
        }

        stage('Build Environment Validation') {
            when {
                expression {
                    return !(env.GIT_BRANCH?.contains('develop') ||
                             env.GIT_BRANCH?.contains('release/') ||
                             env.GIT_BRANCH?.contains('main'))
                }
            }
            steps {
                echo "Build pipeline executed for feature branch or pull request validation on ${env.GIT_BRANCH}"
            }
        }

        stage('Deploy to Dev') {
            when {
                expression {
                    return env.GIT_BRANCH?.contains('develop')
                }
            }
            steps {
                echo "Deploying database to dev environment from ${env.GIT_BRANCH}"
            }
        }

        stage('Deploy to Staging') {
            when {
                expression {
                    return env.GIT_BRANCH?.contains('release/')
                }
            }
            steps {
                echo "Deploying database to staging environment from ${env.GIT_BRANCH}"
            }
        }

        stage('Prod Approval') {
            when {
                expression {
                    return env.GIT_BRANCH?.contains('main')
                }
            }
            steps {
                input message: 'Approve deployment to production?', ok: 'Deploy'
            }
        }

        stage('Deploy to Prod') {
            when {
                expression {
                    return env.GIT_BRANCH?.contains('main')
                }
            }
            steps {
                echo "Deploying database to production environment from ${env.GIT_BRANCH}"
            }
        }
    }
}
