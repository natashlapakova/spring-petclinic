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
        post {
               always {
                         junit 'junit-test/*.xml'
                      }
            }
        }
       stage('SonarQube analysis') {
           withSonarQubeEnv('SonarQube') {
             // requires SonarQube Scanner for Maven 3.2+
             echo 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
           }
         }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
