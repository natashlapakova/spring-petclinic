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
                     emailext attachLog: true, attachmentsPattern: 'generatedFile.txt',
                        body: '${SCRIPT, template="groovy-html.template"}', 
                        mimeType: 'text/html',
                        recipientProviders: [culprits()],
                        subject: '[Jenkins job failed] ${jobName}'
                }
            }
       }

        stage('Build') {
            steps {
                script{
                    currentBuild.displayName = VersionNumber  versionNumberString: '${BUILD_YEAR}-${BUILD_DAY}-${BUILDS_TODAY}-${BUILDS_THIS_YEAR}',
                        projectStartDate: '2019-04-01',                       
                        versionPrefix: 'Pet', worstResultForIncrement: 'SUCCESS'
                }
               
        }
    }
   }
}
