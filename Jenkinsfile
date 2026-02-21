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
                    mvn clean package -Dmaven.test.skip=true
                """
            }
        }

        stage("SONAR_SCANNING"){
            steps{
                dir('./backend') {
                    withCredentials([string(credentialsId: 'sonar_token', variable: 'SONAR_TOKEN')]) {
                        sh """
                           pwd
                           ls -lrt
                           sonar-scanner -Dsonar.token=$SONAR_TOKEN -Dsonar.host.url=http://13.233.127.65:9000/
                        """
                    }       
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