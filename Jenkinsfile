import groovy.json.JsonSlurperClassic
def jsonParse(def json) {
    new groovy.json.JsonSlurperClassic().parseText(json)
}
pipeline {
    agent any
    stages {
        stage("Paso 1: Compilar"){
            steps {
                script {
                sh "echo 'Compile Code!'"
                // Run Maven on a Unix agent.
                sh "./mvnw clean compile -e"
                }
            }
        }
        stage("Paso 2: Testear"){
            steps {
                script {
                    sh "echo 'Test Code!'"
                    // Run Maven on a Unix agent.
                    sh "./mvnw clean test -e"
                }
            }
        }
        stage("Paso 3: Build .Jar step"){
            steps {
                script {
                sh "echo 'Build .Jar!'"
                // Run Maven on a Unix agent.
                sh "./mvnw clean package -e"
                }
            }
        }
        stage("Paso 4: Análisis SonarQube"){
            steps {
                // withSonarQubeEnv('sonarqube') {
                //     sh "echo 'Calling sonar Service in another docker container!'"
                //     // Run Maven on a Unix agent to execute Sonar.
                //     sh './mvnw clean verify sonar:sonar -Dsonar.projectKey=custom-project-key -Dsonar.projectName=custom-project-key'
                // }
                script {
                    sh "echo 'Ejecute Sonar, si claro!'"
                }
            }
        }
        stage("Paso 5: Test de Newman"){
            steps {
                script{
                    // sh "sleep 20 && newman run /home/ejemplo-maven.postman_collection.json"
                    newman run ejemplo-maven.postman_collection.json
                }
            }
        }
    }
    post {
        always {
            sh "echo 'fase always executed post'"
        }
        success {
            sh "echo 'fase success'"
        }
        failure {
            sh "echo 'fase failure'"
        }
    }
}