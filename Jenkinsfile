pipeline {
    agent any
    
    
    environment { 
        NODE_ENV = 'production'
    }
    
    stages {
        stage('Hello') {
            steps {
                sh "echo 'Hello World'"
                sh "env"
                sh "ls"
            }
        }
        stage('Second stage') {
            steps {
                sh "echo 'a hello world from the second step'"
            }
        }
        stage('Display file content') {
            steps {
                sh "cat NOTES.txt"
            }
        }
        
        stage('Call an sh file') {
            steps {
                sh './start-app.sh'
            }
        }
    }
}
