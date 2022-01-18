pipeline {
    agent any

    stages {
        stage('Compile') {
         steps {
                script {
                sh './mvnw.cmd clean compile -e'
                }
            }
        }
        stage('Test') {
            script {
                 steps {
                sh './mvnw.cmd clean test -e'
                }
            }
        }
        stage('Jar') {
            steps {
                 script {
                sh './mvnw.cmd clean package -e'
                 }
            }
        }
        stage('SonarQube analysis'){
            steps{
                script{
                    def scannerHome = tool 'sonar-scanner';
                    withSonarQubeEnv('sonnarqube-server'){
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=ejemplo-maven -Dsonar.sources=src -Dsonar.java.binaries=build"
                    }
                }
            }
        }
        stage('uploadNexus') {
            steps {
                script {
                sh './mvnw.cmd spring-boot:run'
                }
            }
         }
    }
}
