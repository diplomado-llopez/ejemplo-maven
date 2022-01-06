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
        stage('Run') {
            steps {
                script {
                sh './mvnw.cmd spring-boot:run'
                }
            }
         }
        stage('TestingAPP') {
            steps {
                script {
                sh "curl -X GET 'http://localhost:8081/rest/mscovid/test?msg=testing'"
                }
            }
        }
    }
}
