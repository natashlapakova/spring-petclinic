pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                echo 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
