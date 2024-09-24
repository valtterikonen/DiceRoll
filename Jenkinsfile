pipeline {
    agent any
    tools {
        maven 'maven'  // Ensure Maven is installed
        jdk 'JDK21'     // Ensure JDK is installed
    }
    stages {
         stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', 
                    branches: [[name: '*/master']], 
                    userRemoteConfigs: [[url: 'git@github.com:valtterikonen/DiceRoll.git', 
                    credentialsId: 'your-credentials-id']]
                ])
            }
         }
        stage('Build') {
            steps {
                bat 'mvn clean package'
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

