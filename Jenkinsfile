pipeline{
    agent any
   
    stages {
        stage('Clone Repo') {
            
            steps {

                sh "rm -rf *"
                sh "git clone https://github.com/RajDevO/custom-cicd.git"
                       
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                  sh 'docker build -t kuberaj/my-app-2.0 .'
                }
            }
        }
        stage('Deploy Docker Image') {
            steps {
                script {
                 withCredentials([string(credentialsId: 'kuberaj', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u kuberaj -p ${dockerhubpwd}'
                 }  
                 sh 'docker push kuberaj/my-app-2.0'
                }
            }
        }
    }
}

