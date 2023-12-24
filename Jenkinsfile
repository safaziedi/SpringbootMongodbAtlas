pipeline {
    agent any
    tools {
        maven 'maven_3.9.5'
        dockerTool 'docker'
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhubpwdForjenkins')
    }
    stages {
        stage('Get Code from Github & clean workspace') {
                steps {
                    // Clean before build
                    cleanWs()
                    // We need to explicitly checkout from SCM here
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/safaziedi/SpringbootMongodbAtlas']])
                }
        }

        stage('Build maven'){
            steps{
                dir('./back') {
                    sh 'mvn clean package'
                     archiveArtifacts artifacts: 'target/*.jar', onlyIfSuccessful: true
                }
            }
        }
    }}