pipeline {
    agent { label 'docker_builder' }
    triggers {
        pollSCM('* * * * *')
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker_hub_login') 
    }

    stages {
        stage('SCM') {
            steps {
                git branch: 'dev', url: 'https://github.com/shashikamle/spring-petclinic.git'
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t shashikamle/spc .'
            }
        } 
        stage('Docker login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push') {
            steps {
                sh 'docker push shashikamle/spc'
            }
        }
        stage('Deploy on k8s') {
            steps {
                sh 'kubectl apply -f spring.yml'
            }
        }  
    }     
}
