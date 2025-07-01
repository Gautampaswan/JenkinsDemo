pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                bat 'mvn clean install'
            }
        }

        stage('Run') {
            steps {
                echo 'Running the project or tests...'
                bat 'mvn test'
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
