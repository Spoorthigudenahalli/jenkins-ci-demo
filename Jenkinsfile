
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
                echo 'Java project is ready'
                bat 'cd'
                bat 'dir'
            }
        }

        stage('Maven Build and Test') {
            steps {
                bat 'mvn -f C:\\CI\\jenkins-ci-demo\\pom.xml clean test'
            }
        }

        stage('Gradle Build and Test') {
            steps {
                bat 'gradle -p C:\\CI\\jenkins-ci-demo clean test'
            }
        }

        stage('Maven Package') {
            steps {
                bat 'mvn -f C:\\CI\\jenkins-ci-demo\\pom.xml package'
            }
        }
    }

    post {
        always {
            junit allowEmptyResults: true,
                testResults: 'C:/CI/jenkins-ci-demo/target/surefire-reports/*.xml'

            junit allowEmptyResults: true,
                testResults: 'C:/CI/jenkins-ci-demo/build/test-results/test/*.xml'
        }

        success {
            echo 'CI PIPELINE COMPLETED SUCCESSFULLY!'
        }

        failure {
            echo 'CI PIPELINE FAILED!'
        }
    }
}
