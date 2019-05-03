pipeline {
    agent any

 tools {
        maven 'Maven-3.6.1_AUTO'
        jdk 'JDK8_LOCAL'
    }
    stages {
       stage('Complile') {
                   steps {
                       bat 'mvn clean compile'
                   }
       }

       stage('Test and SonarQube analysis') {
           steps {
               bat 'mvn test'
                withSonarQubeEnv('SonarQube-6.7.7') {
                   bat 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
                 }
           }
            post {
                always {
                    junit 'target/surefire-reports/**/*.xml'
                }
                failure {
                    echo 'This will run only if failed'
                }
            }
       }

        stage('Build') {
            steps {
               script {
                         env.currentVersion = '1.0.0' + currentBuild.number
                         currentBuild.displayName = env.currentVersion
                       }
        }
    }
   }
}
