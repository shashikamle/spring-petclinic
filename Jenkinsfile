pipeline {
    agent { label 'k8s_cluster' }
    stages {
        stage('SCM') {
            steps {
                git branch: 'qa', url: 'https://github.com/shashikamle/spring-petclinic.git'
            }
        }
        stage('K8s pull') {
            steps {
                sh 'kubectl apply -f spring.yml'
            }
        }  
    }
}
