pipeline {
    agent { label 'jenkins-slave' }
    tools {
        maven 'MAVEN3.8.7'
    }
    parameters {
     string defaultValue: 'no', description: 'if ready to deploy version2 of your application  then type "yes" otherwise leave it.', name: 'springversion2'
     choice choices: ['0', '1'], description: 'if version2 gets approved and ready for to access by end users select choice \'1\'', name: 'version2'
    }
    stages{
        stage('GitHub-webhook'){
            steps{
                script{
                    properties([pipelineTriggers([githubPush()])])
                }
            }
        }
        stage('Git-clone'){
            steps {
                git branch: 'FIRST', url: 'https://github.com/chaithanya1812/test8-dockerswarm-3-tier-.git'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('dockerlogin and docker build-V1'){
             when {
                expression { "${params.springversion2}" == "no" }
            }
            steps {
            withCredentials([string(credentialsId: 'ddockerloginn', variable: 'dockerlogin')]) {
                sh 'docker login -u chaitu1812 --password $dockerlogin || true'    
              }
               sh 'docker build -t chaitu1812/springboot:v1.0 .'
               sh 'docker push chaitu1812/springboot:v1.0'
            }
        }
        stage('docker build-V2'){
            when {
                expression { "${params.springversion2}" == "yes" }
            }
            steps {
            withCredentials([string(credentialsId: 'ddockerloginn', variable: 'dockerlogin')]) {
                sh 'docker login -u chaitu1812 --password $dockerlogin || true'    
              }
               sh 'docker build -t chaitu1812/springboot:v2.0 .'
               sh 'docker push chaitu1812/springboot:v2.0'
            }
        }
        
        stage("Deploying version-1"){
             when {
                expression { "${params.springversion2}" == "no" }
            }
            steps{
                sshagent(credentials: ['dockerswarm'], ignoreMissing: true) {
                        sh "scp -o StrictHostKeyChecking=no chaitu.yaml ubuntu@13.232.1.17:/home/ubuntu/" 
                        sh "ssh -o StrictHostKeyChecking=no ubuntu@13.232.1.17 docker stack deploy -c chaitu.yaml c1"  
                }
            }
        }
        stage("Deploying version-2"){
             when {
                expression { "${params.springversion2}" == "yes" }
            }
            steps{
                sshagent(credentials: ['dockerswarm'], ignoreMissing: true) {
                        sh "scp -o StrictHostKeyChecking=no chaitu1.yaml ubuntu@13.232.1.17:/home/ubuntu/" 
                        sh "ssh -o StrictHostKeyChecking=no ubuntu@13.232.1.17 docker stack deploy -c chaitu1.yaml c1"  
                }
            }
        }
         stage('Nginx-server-version1'){
             when {
                expression { "${params.version2}" == '0' }
            }
            steps{
                   sshagent(['nginx']) {
                    sh "scp -o StrictHostKeyChecking=no nginx.conf ec2-user@13.232.210.29:/etc/nginx/nginx.conf"
                    sh "ssh -o StrictHostKeyChecking=no ec2-user@13.232.210.29 sudo systemctl restart nginx"
               }
            }
         }
         stage('Nginx-server-version2'){
             when {
                expression { "${params.version2}" == '1' }
            }
             
            steps{
                   sshagent(['nginx']) {
                    sh "scp -o StrictHostKeyChecking=no nginx.conf ec2-user@13.232.210.29:/etc/nginx/nginx.conf"
                    sh "ssh -o StrictHostKeyChecking=no ec2-user@13.232.210.29 sudo systemctl restart nginx"
               }
            }
         }
    }     
}
