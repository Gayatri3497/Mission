pipeline {
    agent any
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
      
      environment{
          SCANNER_HOME = tool 'sonar-scanner'
      }
    stages {
        stage('git checkout') {
            steps {
                git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/Gayatri3497/Mission.git'
            }
        }
        stage('install') {
            steps {
                sh "mvn clean install -DskipTests"
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Mission \
                    -Dsonar.java.binaries=. \
                    -Dsonar.projectKey=Mission '''
                }
            } 
        }
    }
}
