pipeline {
    agent any

    stages {
        stage('install-pip-deps') {
            steps {
                installDependencies()
            }
        }
        stage('deploy-to-dev') {
            steps {
                deploy('dev', 7001)
            }
        }
        stage('tests-on-dev') {
            steps {
                runTests('dev', 'greetings')
            }
        }
        stage('deploy-to-staging') {
            steps {
                deploy('staging', 7002)
            }
        }
        stage('tests-on-staging') {
            steps {
                runTests('staging', 'greetings')
            }
        }
        stage('deploy-to-preprod') {
            steps {
                deploy('preprod', 7003)
            }
        }
        stage('tests-on-preprod') {
            steps {
                runTests('preprod', 'greetings')
            }
        }
        stage('deploy-to-prod') {
            steps {
                deploy('prod', 7004)
            }
        }
        stage('tests-on-prod') {
            steps {
                runTests('prod', 'greetings')
            }
        }
    }
}

def installDependencies() {
    echo 'Installing all required python dependencies...'
    git poll: false, url: 'https://github.com/mtararujs/python-greetings.git'
    powershell 'dir'
    powershell 'pip install -r requirements.txt'
}

def deploy(String environment, int port) {
    echo "Deployment to $environment has started."
    git poll: false, url: 'https://github.com/mtararujs/python-greetings.git'
    powershell "pm2 delete python-micro-service-$environment & set \"errorlevel=0\""
    powershell "pm2 start app.py --name python-micro-service-$environment -- --port $port"
    echo "Deployment to $environment has finished."
}

def runTests(String environment, String testSetName) {
    echo "Running test set \"$testSetName\" in $environment environment..."
    git poll: false, url: 'https://github.com/mtararujs/course-js-api-framework.git'
    powershell 'npm install'
    powershell "npm run $testSetName greetings_$environment"
}
