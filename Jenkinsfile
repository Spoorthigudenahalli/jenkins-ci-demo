
pipeline {
    agent any

    tools {
        jdk 'JDK21'
        maven 'Maven-3.10'
        gradle 'Gradle-9.2.1'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code from GitHub'
                bat 'dir'
            }
        }

        stage('Maven Build and Test') {
            steps {
                echo 'Running Maven tests'
                bat 'mvn clean test'
            }
        }

        stage('Gradle Build and Test') {
            steps {
                echo 'Running Gradle tests'
                bat 'gradle clean test'
            }
        }

        stage('Maven Package') {
            steps {
                echo 'Packaging Java application'
                bat 'mvn package'
            }
        }

        stage('Archive JAR Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar',
                                 fingerprint: true
            }
        }
    }

    post {
        always {
            echo 'Publishing test reports'

            junit allowEmptyResults: true,
                testResults: 'target/surefire-reports/*.xml'

            junit allowEmptyResults: true,
                testResults: 'build/test-results/test/*.xml'
        }

        success {
            echo 'CI PIPELINE COMPLETED SUCCESSFULLY!'
            echo 'JAR artifact archived successfully!'
        }

        failure {
            echo 'CI PIPELINE FAILED!'
        }
    }
}
