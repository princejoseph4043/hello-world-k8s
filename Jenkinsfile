pipeline {
    agent {
        node {
            label 'slave01'
            def ecRegistry      = "https://122910936396.dkr.ecr.us-east-1.amazonaws.com"
            def remoteImageTag  = "v_${BUILD_NUMBER}"
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

    stage("Docker push") {
    docker.withRegistry(ecRegistry, "ecr:us-east-1:aws-ecr-credential") {
          docker.image("apache-alpine:${remoteImageTag}").push(remoteImageTag)
    }
    
    }

    }

}