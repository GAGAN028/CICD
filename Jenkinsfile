pipeline {
    agent any
    stages {
        stage("CHECKOUT"){
            steps{
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        credentialsId: 'github',
                        url: 'https://github.com/GAGAN028/CICD.git'
                    ]]
                ])
            }
        }

        stage("CHECKOUT"){
            steps{
                sh """
                    pwd
                    ls -lrt
                """
            }    
        }        
    }
}
