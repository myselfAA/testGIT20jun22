pipeline {
    agent {
      node {
            label 'slave1'
           }
    }

    stages {
        stage('checkout code') {
            steps {
                echo 'retrieving code from GIT'
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/koddas/war-web-project.git']])
            }
        }
        stage('build') {
            steps {
                echo 'building the code'
                sh 'mvn clean install'
            }
        }
        stage('Deployment') {
            steps {
                echo 'Deploying to container'
                deploy adapters: [tomcat8(credentialsId: 'tomcat/tomcat', path: '', url: 'http://172.31.19.81:8088')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
