pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the Git repository using the specified credentials
                checkout([$class: 'GitSCM', 
                    branches: [[name: '*/master']], 
                    userRemoteConfigs: [[
                        url: 'git@github.com:valtterikonen/DiceRoll.git', // Replace with your actual repository URL
                        credentialsId: '15a8b23c-fc66-4153-82e7-aff21538f3be' // Your credentials ID
                    ]]
                ])
            }
        }
        stage('Build') {
            steps {
                // Add your build steps here, e.g., Maven or Gradle build
                sh 'mvn clean install' // Example for Maven
            }
        }
        stage('Run Unit Tests') {
            steps {
                // Add steps to run your unit tests here
                sh 'mvn test' // Example for running tests with Maven
            }
        }
        stage('Code Coverage Report') {
            steps {
                // Add steps to generate and publish code coverage report
                sh 'mvn cobertura:cobertura' // Example for code coverage
            }
        }
    }
    post {
        always {
            // Steps that will run regardless of build success or failure
            echo 'Pipeline completed.'
        }
        success {
            // Steps that will run if the build is successful
            echo 'Build completed successfully!'
        }
        failure {
            // Steps that will run if the build fails
            echo 'Build failed. Check the logs for more details.'
        }
    }
}

