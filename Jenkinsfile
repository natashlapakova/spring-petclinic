pipeline {
    agent any

 tools {
        maven 'Maven-3.6.1'
    }
    stages {
       stage('Complile') {
                   steps {
                       bat 'mvn clean compile'
                   }
       }

       stage('Test') {
           steps {
               bat 'mvn test'
           }
            post {
                always {
                junit 'target/surefire-reports/**/*.xml'
                }
            }
       }

       stage('SonarQube analysis') {
           steps{
                   withSonarQubeEnv('SonarQube-6.7.7') {
                     bat 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
                   }
               }
         }

        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
