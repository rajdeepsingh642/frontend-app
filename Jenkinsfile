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
        
  
        
       
        
    
      
     
        stage('Deploy to Conatiner') {
            steps {
                sh "docker build -t frontend ."
                sh "docker run -d 8081:8081 --name frontend frontend"
            }
        }
    }
}