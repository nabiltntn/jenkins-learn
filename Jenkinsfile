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
                sh 'chmod +x ./start-app.sh'
                sh './start-app.sh'
            }
        }
        stage('Test multiline') {
            steps {
                sh '''
                echo "echo first line"
                echo "second line again"
                echo "third line again"
                # force an exit code to test displaying the post message in any case
                # exit 1
                '''
            }
        }
        
        }        
        post {
            // it's possible to have as much level as we want to trigger some process in certain cases
            always {
                sh "echo i wil alaways say a by message at the end"
                sh "echo make call to outside application"
            }
            
            failure {
                sh 'echo "make special call when error happens"'
            }
        }
        

}
