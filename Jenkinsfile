pipeline {
    agent any

    environment {
        BROWSERSTACK_USERNAME = 'chiragpaswan_wQh5KY'
        BROWSERSTACK_ACCESSKEY = '9zahoZzNwyhD41n1GhsP'
    }

    tools {
        maven 'Maven'  // 👈 This should match the name you gave in Global Tool Configuration
    }

    triggers {
        cron('H H 1 1 * 
')  // Run every 2 minutes
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Run Tests on BrowserStack') {
            steps {
                sh '''
                    mvn clean test \
                    -Dbrowserstack=true \
                    -Dbrowserstack.user=$BROWSERSTACK_USERNAME \
                    -Dbrowserstack.key=$BROWSERSTACK_ACCESSKEY
                '''
            }
        }
    }

    post {
        always {
            echo 'Build finished.'
        }
        success {
            echo '✅ Test passed!'
        }
        failure {
            echo '❌ Build failed!'
        }
    }
}
