pipeline {
    agent { label 'agent-2'}
    
    tools {
        maven 'Maven-3.9.11'
        jdk 'jdk17'
    }

    stages {
        
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
        
        stage('Test') {
            steps {
               sh 'mvn test'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn package'
            }
        }
    }
}