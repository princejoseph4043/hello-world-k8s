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

        stage ('Docker_Push') {
        docker.withRegistry('https://897585983198.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:aws-ecr-credential') {
            docker.image('apache-alpine').push('latest')
        }

    }

    }

}