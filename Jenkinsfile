pipeline {
    agent any
    tools{
        maven 'maven-3.9.3'
        jdk 'jdk-17'
    }

    environment{
        SCANNER_HOME= tool 'sonar-scanner'
            }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/chianeng-tech-org/wordsmith-api.git'
            }
        }

        stage('Code Compile') {
            steps {
                sh "mvn clean compile"
            }
        }

        stage('Test Cases') {
            steps {
                sh "mvn test"
            }
        }

        stage('Sonar Analysis') {
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar Dsonar.projectKey=api'
                    
                    
                }
            }
        }
    }
}
