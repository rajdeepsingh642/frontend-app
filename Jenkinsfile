pipeline {
    agent any
    
    tools{
        jdk 'jdk17'
        nodejs 'node16'
        
    }
    
    environment{
        SCANNER_HOME= tool 'sonar-scanner'
    }
    
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/jaiswaladi246/fullstack-bank.git'
            }
        }
        
        stage('OWASP FS SCAN') {
            steps {
                dependencyCheck additionalArguments: '--scan .--disableYarnAudit --disableNodeAudit', odcInstallation: 'DC'
                    dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        
       
        
        stage('SONARQUBE ANALYSIS') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh " $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Bank -Dsonar.projectKey=Bank "
                }
            }
        }
        
        
         stage('Install Dependencies') {
            steps {
                sh "npm install"
            }
        }
        
      
        
        stage('frontend') {
            steps {
                dir('/root/.jenkins/workspace/Bank/app/frontend') {
                    sh "npm install"
                }
            }
        }
        
        stage('Deploy to Conatiner') {
            steps {
                sh "docker build -t frontend ."
                sh "docker run -d 8081:8081 --name frontend frontend"
            }
        }
    }
}