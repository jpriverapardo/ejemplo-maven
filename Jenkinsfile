import groovy.json.JsonSlurperClassic
def jsonParse(def json) {
    new groovy.json.JsonSlurperClassic().parseText(json)
}
pipeline {
    agent any
    stages {
         stage("Paso 1: Build && Test"){
            steps {
                script{
                    sh "echo 'Build && Test!'"
                    sh "./mvnw clean package -e"    
                }
            }
        }

        stage("Paso 2: Sonar - Análisis Estático"){
            steps {
                script{
                    sh "echo 'Análisis Estático!'"
                        withSonarQubeEnv('sonarqube') {
                            sh "echo 'Calling sonar by ID!'"
                            // Run Maven on a Unix agent to execute Sonar.
                            sh './mvnw clean verify sonar:sonar -Dsonar.projectKey=ejemplo-maven-full-stages -Dsonar.projectName=cejemplo-maven-full-stages -Dsonar.java.binaries=build'
                        }
                        
                }
            }
        }
        
        stage("Paso 3: Curl Springboot maven sleep 20"){
            steps {
                script{
                    sh "nohup bash ./mvnw spring-boot:run  & >/dev/null"
                    sh "sleep 20 && curl -X GET 'http://localhost:8081/rest/mscovid/test?msg=testing'"
                }
            }
        }
        stage("Paso 4: Test de Newman"){
            steps {
                script{
                    sh "newman run ejemplo-maven.postman_collection.json"
                }
            }
        }
        stage("Paso 5: Detener Spring Boot"){
            steps {
                script{
                    sh '''
                        echo 'Process Spring Boot Java: ' $(pidof java | awk '{print $1}')  
                        sleep 20
                        kill -9 $(pidof java | awk '{print $1}')
                    '''
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