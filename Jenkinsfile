pipeline {
    agent any
    tools {
        maven 'maven'
       }
    stages {
        stage('gitcheckout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/teja2894/hello-teja.git']])
            }
        }
        stage('build and push docker image') {
            steps {
               withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'PASSWD', usernameVariable: 'USERNAME')]) {
                sh 'docker login -u ${USERNAME} -p ${PASSWD}'
                sh 'docker build -t hello-world .'
                sh 'docker tag hello-world tejaswi2894/hello'
                sh 'docker push tejaswi2894/hello'
               }
            }
        } 
    }
}
