pipeline {
    agent any
    tools {
        jdk 'JDK17'      // Name you gave your JDK in Jenkins Tools config
        maven 'Maven3'   // Name you gave your Maven in Jenkins Tools config
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build & Test') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'mvn clean test'
                        sh 'mvn package'
                    } else {
                        bat 'mvn clean test'
                        bat 'mvn package'
                    }
                }
            }
        }
        stage('Archive') {
            steps {
                junit 'target/surefire-reports/*.xml'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}



