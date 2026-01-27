pipeline{
    agent any
    // tools {
    //     maven "maven_main"
    // }

    // environment {
    //     BACKEND_IMAGE = "harshajain/backend"
    //     DOCKERFILE_BACKEND = "./Dockerfile"
    // }

    stages{
        stage("CHECKOUT"){
            steps{
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        credentialsId: 'github',
                        url: 'https://github.com/GAGAN028/GA_demo'
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

        // stage("SONAR_SCANNING") {
        //     steps {
        //         dir('./backend') {
        //             withCredentials([string(credentialsId: 'backend', variable: 'SONAR_TOKEN')]) {
        //                 sh '''
        //                     pwd
        //                     ls -lrt  
        //                     sonar-scanner -Dsonar.host.url=http://65.0.129.172:9000
        //                 '''
        //             }
        //         }
        //     }
        // }


        // stage('BUILD AND PUSH') {
        //     steps {
        //         script {
        //             dir('./backend') {
        //                 def backendImage = docker.build("${BACKEND_IMAGE}:${env.BUILD_NUMBER}", "-f ${env.DOCKERFILE_BACKEND} .")
        //                 docker.withRegistry('https://registry.hub.docker.com','docker_hub') {
        //                     backendImage.push()
        //                 }
        //             }
        //         }
        //     }
        // }


        // stage('DEPLOY TO K8S') {
            
        // }

    }
    // post {
    //     always {
    //         cleanWs()
    //     }
    // }
}
