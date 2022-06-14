node {
    def mvnHome = tool 'MyMaven'
    def dockerImageTag = "zeruyang001/zerudockerhub{env.BUILD_NUMBER}"
    stage('clone repo'){
        git 'https://github.com/zeru427/demo-service.git'
        mvnHome = tool 'MyMaven'
    }
    stage('Build demoservice project'){
        //sh    linux
        bat "C:\\fortest\\Maven\\apache-maven-3.8.5\\bin\\mvn clean install"
        //jar file will be generated
    }
    stage('Build docker image'){
        dockerImage = docker.build("zeruyang001/zerudockerhub:${env.BUILD_NUMBER}")
    }
    stage('Build docker deploy'){
        echo "Docker Image Tag name : ${dockerImageTag}"
        //docker-hub-credentials - we have to create in jenkins credentials
        docker.withRegistry('https://registry.hub.docker.com','docker-hub-credentials') {
            dockerImage.push("${env.BUILD_NUMBER}")
            dockerImage.push("latest")
        }
    }
}