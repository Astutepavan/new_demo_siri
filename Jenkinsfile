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
        stage('scaning') {
            steps {

                // Run Maven on a Unix agent.
                sh "mvn sonar:sonar \
                     -Dsonar.projectKey=demo_test \
                     -Dsonar.host.url=http://54.173.210.207:9000 \
                     -Dsonar.login=54c9e467a491c57056f470da5f3e8187848a6e91"

            }
        }    
        stage('versioning') {
            steps {
                sh "pwd"
                sh "ls ./target"
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'awsuser']]){
                sh "/usr/local/bin/aws s3 cp /var/lib/jenkins/workspace/siri_auto_ci/target/mavewebappdemo-2.0.0-SNAPSHOT.war s3://test-buck-00038938938"}
            }
        }
    }
}