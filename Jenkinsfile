pipeline {
    agent any

    stages {
        stage('checkout code') {
            steps {
                echo 'retrieving code from GIT'
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/boxfuse/boxfuse-sample-java-war-hello.git']])
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
                deploy adapters: [tomcat8(credentialsId: 'admin/admin', path: '', url: 'http://172.31.19.81:8088')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
