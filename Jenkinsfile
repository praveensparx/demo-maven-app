pipeline {
    agent any

    tools {
        jdk 'JDK17'      // Must match Jenkins JDK name
        maven 'Maven-3'  // Must match Jenkins Maven name
    }

    environment {
        // Use the GitHub credential ID you created in Jenkins (PAT)
        GIT_CREDENTIALS = 'github-token'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/praveensparx/demo-maven-app.git',
                    credentialsId: "${GIT_CREDENTIALS}"
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging the application...'
                sh 'mvn package'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the console output for errors.'
        }
    }
}
