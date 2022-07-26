pipeline {
    agent none
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker_hub_login') 
    }

    stages {
        stage('SCM') {
            agent { label 'docker_builder' && 'k8s_cluster' }
            steps {
                git branch: 'dev', url: 'https://github.com/shashikamle/spring-petclinic.git'
            }
        }
        stage('Build') {
            agent { label 'docker_builder' }
            steps {
                sh 'docker build -t shashikamle/spc .'
            }
        } 
        stage('Docker login') {
            agent { label 'docker_builder' }
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push') {
            agent { label 'docker_builder' }
            steps {
                sh 'docker push shashikamle/spc'
            }
        }
        stage('K8s pull') {
            agent { label 'k8s_cluster' }
            steps {
                sh 'kubectl apply -f spring.yml'
            }
        }  
    }     
}
