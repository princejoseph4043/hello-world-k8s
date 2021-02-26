pipeline {
    agent {
        node {
            label 'testing'
        }
    }
    
    stages {       
        stage('Prepare') {
            steps {
                checkout([$class: 'GitSCM',
                branches: [[name: "origin\main"]],
                doGenerateSubmoduleConfigurations: false,
                submoduleCfg: [],
                userRemoteConfigs: [[
                    url: 'https://github.com/princejoseph4043/hello-world-k8s.git']]
                ])
            }
        }
    }
}