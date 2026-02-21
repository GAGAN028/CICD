pipeline{
    agent any
    tools {
        maven "maven_main"
    }

    stages{
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
                sh """
                    mvn clean compile
                """
            }
        }

        stage("SONAR_SCANNING"){
            steps{
                dir('./backend') {
                    withCredentials([string(credentialsId: 'sonar-server', variable: 'SONAR_TOKEN')]) {
                        sh """
                            sonar-scanner \
                            -Dsonar.projectKey=java \
                            -Dsonar.projectName=java \
                            -Dsonar.host.url=http://13.233.127.65:9000 \
                            
                        """
                    }       
                }  
            }    
        }        
    }

    post {
       always {
            cleanWs()
        }
    }
}