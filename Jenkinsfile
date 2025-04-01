pipeline {
    agent any

    stages {
        stage('install-pip-deps') {
            steps {
                echo 'Installing python dependencies...'
            }
        }
        stage('build') {
            steps {
                echo 'Building micro-service...'
            }
        }
        stage('deploy-to-dev') {
            steps {
                deploy('dev')
            }
        }
        stage('tests-on-dev') {
            steps {
                runTests('dev')
            }
        }
        stage('deploy-to-staging') {
            steps {
                deploy('staging')
            }
        }
        stage('tests-on-staging') {
            steps {
                runTests('staging')
            }
        }
        stage('deploy-to-preprod') {
            steps {
                deploy('preprod')
            }
        }
        stage('tests-on-preprod') {
            steps {
                runTests('preprod')
            }
        }
        stage('deploy-to-prod') {
            steps {
                deploy('prod')
            }
        }
        stage('tests-on-prod') {
            steps {
                runTests('prod')
            }
        }
    }
}

def deploy(String environment) {
    echo "Deploying to ${environment} environment..."
}

def runTests(String environment) {
    echo "Running tests in ${environment} environment..."
}
