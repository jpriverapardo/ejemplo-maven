pipeline {
    agent any

    stages {
        stage('Compile Code') {
            steps {
                ./mvnw.cmd clean compile -e
            }
        }
        stage('Test Code') {
            steps {
                ./mvnw.cmd clean test -e
            }
        }
        stage('Jar Code') {
            steps {
                ./mvnw.cmd clean package -e
            }
        }
        stage('Run Jar') {
            steps {
                ./mvnw.cmd spring-boot:run
                // nohup bash mvnw.cmd spring-boot:run &
            }
        }
        stage('Testing Application') {
            steps {
                // ./mvnw.cmd spring-boot:run
                curl -X GET 'http://localhost:8081/rest/mscovid/test?msg=testing'
            }
        }
    }
}


Test Code
./mvnw.cmd clean test -e
Jar Code
./mvnw.cmd clean package -e
Run Jar
Local: ./mvnw.cmd spring-boot:run
Background: nohup bash mvnw.cmd spring-boot:run &
Testing Application
Abrir navegador: http://localhost:8081/rest/mscovid/test?msg=testing