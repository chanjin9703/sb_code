pipeline {
    agent any
    tools {
        maven 'my_maven'
    }
    environment {
        GITNAME = 'chanjin9703' 
        GITEMAIL = 'ks3ppp@gmail.com'
        GITWEBADD = 'https://github.com/chanjin9703/sb_code.git'
        GITSSHADD = 'git@github.com:chanjin9703/sb_code.git'
        GITCREDENTIAL = 'git_cre'
    }    
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}