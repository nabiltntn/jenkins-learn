pipeline {
    agent any
    
    
    environment { 
        NODE_ENV = 'production'
    }
    
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                env
                ls
            }
        }
        stage('Second stage') {
            steps {
                echo 'a hello world from the second step'
            }
        }
    }
}
