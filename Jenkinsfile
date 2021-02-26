pipeline {
    agent {
        node {
            label 'slave01'
        }
    }
    
    stages {       
        stage('Prepare') {
            steps {
                checkout([$class: 'GitSCM', 
                branches: [[name: '*/main']], 
                extensions: [], 
                userRemoteConfigs: [[
                    url: 'https://github.com/princejoseph4043/hello-world-k8s.git']]
                ])

            }
        }
    
    stage ('Docker_Build') {
            steps {
                sh '''cd docker
                docker build -t apache-alpine .'''
            }
    }
}