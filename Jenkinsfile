pipeline {

    options {
        buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '5'))
    }
    agent any

    tools {
        maven 'maven_3.0.5'
    }

    stages {
        stage('Code Compilation') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
           steps {
                sh 'docker build -t best .'
           }
         }


    }
}