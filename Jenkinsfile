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
    }

    stage ('Docker_Build') {
            steps {
                \\ Build the docker image
                sh'''
                    # Build the image
                    $(aws ecr get-login --region eu-west-1 --profile global --no-include-email)
                    cd docker
                    docker build . -t apache-alpine
                '''
            }
        }
}