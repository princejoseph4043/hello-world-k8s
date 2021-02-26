pipeline {
    agent {
        node {
            label 'testing'
        }
    }
    
    stage('Clone repository') {
        git branch: "main", url: "https://github.com/princejoseph4043/hello-world-k8s.git"
    }

    
}