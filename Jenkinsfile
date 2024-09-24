pipeline {
    agent any
    tools {
        maven 'maven'  // Ensure Maven is installed
        jdk 'JDK21'     // Ensure JDK is installed
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: "master", url: 'https://github.com/valtterikonen/DiceRoll.git'
            }
        }
        stage('Build') {
            steps {
                withEnv(["JAVA_HOME=C:\\Program Files\\Java\\jdk-21"]) {
                    bat 'mvn clean package'
                }
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
