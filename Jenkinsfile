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
         steps {
                script {
       docker.withRegistry('https://897585983198.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:aws-ecr-credential') {
            docker.image('apache-alpine').push('latest')
              }
               }
       }

       }

        stage ('Deploy_K8S') {
             steps {
 //                    withCredentials([string(credentialsId: "aws-login-credentials", variable: 'ARGOCD_AUTH_TOKEN')]) {
                        sh '''
                        ARGOCD_SERVER="a124d6af24d234dd5889feb1735904cb-1188587285.us-east-1.elb.amazonaws.com"
                        APP_NAME="first-demo"
                        CONTAINER="apache-alpine"
                        REGION="us-east-1"
                        AWS_ACCOUNT="897585983198"
                        AWS_ENVIRONMENT="staging"

#                        $(aws ecr get-login --region $REGION --profile $AWS_ENVIRONMENT --no-include-email)
                        
                        # Deploy image to ECR
 #                       docker tag $CONTAINER:latest $AWS_ACCOUNT.dkr.ecr.$REGION.amazonaws.com\$CONTAINER:latest
 #                       docker push $AWS_ACCOUNT.dkr.ecr.$REGION.amazonaws.com\$CONTAINER:latest
                        IMAGE_DIGEST=$(docker image inspect $AWS_ACCOUNT.dkr.ecr.$REGION.amazonaws.com/$CONTAINER:latest -f '{{join .RepoDigests ","}}')
                        # Customize image 
                        ARGOCD_SERVER=$ARGOCD_SERVER argocd --grpc-web app set $APP_NAME --kustomize-image $IMAGE_DIGEST
                        
                        # Deploy to ArgoCD
                        ARGOCD_SERVER=$ARGOCD_SERVER argocd --grpc-web app sync $APP_NAME --force
                        ARGOCD_SERVER=$ARGOCD_SERVER argocd --grpc-web app wait $APP_NAME --timeout 600
                        '''
               }
            }
        }        



    }