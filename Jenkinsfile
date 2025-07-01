pipeline {
    agent any

    environment {
        MAVEN_HOME = tool 'Maven'       // Name of Maven configured in Jenkins
        PATH = "${MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {

        stage('📥 Clone Code') {
            steps {
                git 'https://github.com/Gautampaswan/JenkinsDemo.git'
            }
        }

        stage('🔧 Build & Install') {
            steps {
                echo 'Cleaning and installing project dependencies...'
                bat 'mvn clean install'
            }
        }

        stage('🧪 Run Tests') {
            steps {
                echo 'Executing Selenium/TestNG test cases...'
                bat 'mvn test'
            }
        }

        stage('📊 Generate Allure Report') {
            steps {
                echo 'Generating Allure reports...'
                bat 'mvn allure:report'
                allure includeProperties: false, jdk: '', results: [[path: 'allure-results']]
            }
        }
    }

    post {
        success {
            echo '🎉 Build Succeeded!'
            mail to: 'paswangkp506@gmail.com',
                 subject: "✔️ SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "✅ Jenkins build succeeded!\n\nCheck console output: ${env.BUILD_URL}"
        }

        failure {
            echo '❌ Build Failed!'
            mail to: 'paswangkp506@gmail.com',
                 subject: "❌ FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "⚠️ Jenkins build failed.\n\nCheck console output: ${env.BUILD_URL}"
        }
    }
}
