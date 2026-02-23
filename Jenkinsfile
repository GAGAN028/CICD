pipeline {
    agent any

    tools {
        maven "maven_main"
    }

    stages {

        stage("CHECKOUT"){
            steps{
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        credentialsId: 'github',
                        url: 'https://github.com/GAGAN028/GA_demo.git'
                    ]]
                ])
            }
        }

        stage("Maven Build") {
            steps {
                sh "mvn clean compile"
            }
        }

        stage("SONAR_SCANNING"){
            steps{
                dir('./backend') {
                    withCredentials([string(credentialsId: 'sonar-server', variable: 'SONAR_TOKEN')]) {
                        sh """
                           pwd
                           ls -lrt
                           sonar-scanner \
                           -Dsonar.projectKey=java \
                           -Dsonar.host.url=http://13.233.127.65:9000 \
                           -Dsonar.login=$SONAR_TOKEN
                        """
                    }       
                }  
            }    
        } 

        stage('BUILD') {
            steps {
            dir('./backend') {
                sh """
                   pwd
                   ls -lrt
                   sudo docker build -t backend:latest
            }   """
        }       
    }

    
    post {
        always {
            cleanWs()
        }
    }
}