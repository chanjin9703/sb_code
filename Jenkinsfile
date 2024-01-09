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
        
        DOCKERHUB = 'ks3ppp/spring'
        DOCKERHUBCREDENTIAL = 'docker_cre'
    }    
    stages {
        stage('Checkout Github') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [],
                userRemoteConfigs: [[credentialsId: GITCREDENTIAL, url: GITWEBADD]]])

            }
        
        
            post {
        
                failure {
                    echo 'Repository clone failure'
                }
                success {
                    echo 'Repository clone success'
                }
            }
        }    
            
        stage('code build') {
            steps {
                sh "mvn clean package"
            }
        }
        stage('image build') {
            steps {
                sh "docker build -t ${DOCKERHUB}:${currentBuild.number} ."
                // currentBuild.numer = 젠킨스가 제공하는 빌드넘버 변수
                //ks3ppp/spring:1 같은 형태로 빌드가 될 것.
            }
        }
        stage('image push') {
            steps {
                sh "docker push ${DOCKERHUB}:${currentBuild.number}"
                sh "docker push ${DOCKERHUB}:latest"
            }
            
            post { 
                failure {
                    echo 'docker image push fail'
                    sh "docker image rm -f ${DOCKERHUB}:${currentBuild.number}"
                    sh "docker image rm -f ${DOCKERHUB}:latest"
                }
                success {
                    echo 'docker image push success'
                    sh "docker image rm -f ${DOCKERHUB}:${currentBuild.number}"
                    sh "docker image rm -f ${DOCKERHUB}:latest"
                }    
                    
        }
    }
}