pipeline {
    agent any

    stages {
        stage('Compile') {
         steps {
                script {
                sh 'chmod +x mvnw'
                sh './mvnw.cmd clean compile -e'
                }
            }
        }
        stage('Test') {
           steps {
            script {
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
                nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'test-nexus', packages: [[$class: 'MavenPackage', mavenAssetList: [], mavenCoordinate: [artifactId: 'DevOpsUsach2020', groupId: 'com.devopsusach2020', packaging: 'jar', version: '0.0.1']]]
            }
         }
    }
}
