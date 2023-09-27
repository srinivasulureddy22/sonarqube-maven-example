pipeline {
    agent any
     tools {
        maven 'maven' 
    }
    stages {
        stage('clone') {
            steps{
               git credentialsId: 'gtihublogin', url: 'https://github.com/srinivasulureddy22/maven-pp.git'
            }
        }
        stage('maven version') {
            steps{
               sh 'mvn --version'
            }
        }
        stage('maven') {
            steps{
               sh 'mvn clean install'
            }
        }
        stage('sonarqube') {
//    def scannerHome = tool 'SonarScanner 4.0';
        steps{
        withSonarQubeEnv('sonar') { 
        // If you have configured more than one global server connection, you can specify its name
//      sh "${scannerHome}/bin/sonar-scanner"
        sh "mvn sonar:sonar"
    }
        }
        }
        stage('deployment') {
           steps{
              deploy adapters: [tomcat9(credentialsId: '32bd3d00-bd53-4698-8b5b-c469be02beca', path: '', url: 'http://13.127.9.171:8080')], contextPath: 'tomcattesting', war: '**/*.war'
            }
        }
    }
}    
