pipeline {
    agent none
    stages {
        stage('SCM') {
            agent { label 'k8s_cluster' }
            steps {
                git branch: 'qa', url: 'https://github.com/shashikamle/spring-petclinic.git'
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
