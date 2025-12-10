pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'M3'
    }

    options {
        timestamps()
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/dmhrov/gs-spring-boot.git'
            }
        }

        stage('Build & Test') {
            steps {
                dir('complete') {
                    sh 'mvn -B clean test'
                }
            }
        }

        stage('Package') {
            steps {
                dir('complete') {
                    sh 'mvn -B package'
                }
            }
        }

        stage('Archive artifacts') {
            steps {
                archiveArtifacts artifacts: 'complete/target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
        }
        failure {
            echo "Build FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
        }
    }
}
