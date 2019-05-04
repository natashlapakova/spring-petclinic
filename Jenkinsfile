pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }

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
               VersionNumber projectStartDate: '2019-04-01', 
                             versionNumberString: '${BUILD_YEAR}-${BUILD_DAY}-${BUILDS_TODAY}-${BUILDS_THIS_YEAR}',
                             versionPrefix: 'Pet', worstResultForIncrement: 'SUCCESS'
        }
    }
   }
}
