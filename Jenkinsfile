pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Clean') {
            steps {
                cleanWs()
            }
        }
        stage('Hello') {
            steps {
                echo 'Bye Bye'
            }
        }
    }
}
