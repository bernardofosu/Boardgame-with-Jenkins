pipeline {
    agent { label 'agent-1'}
    
    tools {
        maven 'Maven-3.9.11'
        jdk 'jdk17'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/bernardofosu/Boardgame-with-Jenkins.git'
            }
        }
        
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