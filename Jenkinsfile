pipeline{
    agent any
   
    stages {
      
        stage('Build Maven') {
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: '32b3b981-5a47-4082-85dd-508e1eeec392', url: 'https://github.com/RajDevO/custom-cicd.git']]])
                sh "mvn -Dmaven.test.failure.ignore=true clean package"         
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

