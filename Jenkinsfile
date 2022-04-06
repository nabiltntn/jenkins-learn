// Complete guide is available here https://www.jenkins.io/doc/book/pipeline/syntax/

pipeline {
    agent any
    
    // how to triggers this pipeline ( with cron expression, pollSCM cron and check if changes to restart , uppstream : impacted  )
    //triggers{
        // start this pipeline every 2 minutes
        //cron('H/2 * * * *')  
    //}
    
    environment { 
        NODE_ENV = 'production'
    }
    
    
    tools {
        maven 'maven-3-8-5' 
    }
    
    options {
        timeout(time: 1, unit: 'HOURS')
        // other options
        // retry ,  disableResume , disableConcurrentBuilds, buildDiscarder ( options for keeping log, build history, etc )
        timestamps()
    }
    
    // add some params for the pipeline
    
    parameters {
        string(name: 'TAG_VERSION', defaultValue: '', description: 'version tag to deploy')   
        // other possibilities
       
        //text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        //booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'ENV', choices: ['INT', 'ACC', 'PROD'], description: 'Destination environnement')

        //password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }
    
    
    stages {
        stage('Hello') {
            steps {
                sh "echo 'Hello World'"
                sh "env"
                sh "ls"
                sh "echo i will do a build in ${params.ENV} with version ${params.TAG_VERSION}"
                sh "mvn --version"
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
            environment { 
                SOME_SPECIAL_ENV = credentials('name-of-application')
            }
            steps {
                sh 'env'
                sh 'chmod +x ./start-app.sh'
                sh './start-app.sh'
                sh 'echo $SOME_SPECIAL_ENV > result.txt'
                sh 'cat result.txt'
                // Use this instruction to save some files are pipeline artifact
                archiveArtifacts artifacts: 'result.txt', fingerprint: true
            }
        }
        stage('Test multiline') {
            // include a manual validation before continue in this step ( speciall for deploying in Poroduction )
            input {
                message "Are you sure to deploy in Production"
                ok "Yes, we should."
            }
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
