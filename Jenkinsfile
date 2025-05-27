pipeline {
    agent any
    stages {
        stage('checkout') {
            steps {
                // Get some code from a GitHub repository
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Astutepavan/new_demo_siri.git']])
            }   
         }

        stage('Build') {
            steps {

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean install"

            }
        }    
        stage('versioning') {
            steps {
                sh "pwd"
                sh "ls ./target"
            }
        }
    }
}