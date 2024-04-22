pipeline {
    agent any
    
    tools{
        jdk 'jdk11'
        nodejs 'node16'
        
    }
    
    
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/rajdeepsingh642/frontend-app.git'
            }
        }
        
        stage('OWASP FS SCAN') {
            steps {
                dependencyCheck additionalArguments: '--scan .--disableYarnAudit --disableNodeAudit', odcInstallation: 'DC'
                    dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
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