pipeline {
    agent any
    tools {nodejs "NodeJS"}
    stages{
        stage('Build npm'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/samzri1/nodejs-docs-hello-world/']]])
                sh ' npm run start'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t samzri/devops-integration2 .'
                }
            }
        }
       
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u samzri -p dckr_pat_kRC0j5zg0C3mJhxQCeigH2xg0BA'}
                   sh 'docker push samzri/devops-integration2'
                }
            }
        }
      //  stage('Deploy to k8s'){
     //       steps{
        //        script{
      //              kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'k8sconfigpwd')
      //          }
       //     }}
    }
}
