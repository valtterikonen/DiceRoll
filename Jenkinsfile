pipeline {
    agent any
    tools {
        maven 'maven'  // Ensure Maven is installed
        jdk 'JDK21'     // Ensure JDK is installed
    }
    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/valtterikonen/DiceRoll.git', branch: 'master'
            }
        }
        stage('List Workspace') {
            steps {
                bat 'dir'  // List files in the workspace
            }
        }
        stage('Build') {
        steps {
                dir('DiceRoll') { // Navigate to the DiceRoll directory
                    script {
                        bat 'mvn clean package -X' // Use -X for debug information
                    }
                }
        }
        }
        stage('Run Unit Tests') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'  // Capture test reports
                }
            }
        }
        stage('Code Coverage Report') {
            steps {
                bat 'mvn jacoco:report'
            }
            post {
                always {
                    jacoco execPattern: 'target/jacoco.exec'
                }
            }
        }
    }
}
