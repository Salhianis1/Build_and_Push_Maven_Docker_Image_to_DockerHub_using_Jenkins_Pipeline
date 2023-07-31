pipeline{
    agent any
    tools {
        maven 'maven-3.9.3'
    }
    stages {
        stage('Build Maven') {
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Salhianis1/Build_and_Push_Maven_Docker_Image_to_DockerHub_using_Jenkins_Pipeline.git']])
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
                
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                  sh 'sudo docker build -t salhianis20/my-app-1.0 .'
                }
            }
        }
        stage('Deploy Docker Image') {
            steps {
                script {
                 withCredentials([string(credentialsId: 'dockerhub_ID', variable: 'dockerhub_pwd')]) {
                    sh 'sudo docker login -u salhianis20 -p ${dockerhub_pwd}'
                 }  
                 sh 'sudo docker push salhianis20/my-app-1.0'
                }
            }
        
}
}
}

