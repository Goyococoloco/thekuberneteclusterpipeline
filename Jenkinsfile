pipeline {
    agent any
    stages {
        stage('Create kubernetes cluster') {
            steps {
                withAWS(region:'us-west-2', credentials:'blueocean') {
                    sh '''
                        eksctl create cluster \
                        --name ekscluster \
                        --version 1.17 \
                        --region us-west-2 \
                        --nodegroup-name eksnodes \
                        --node-type t2.micro \
                        --nodes 2 \
                        --nodes-min 1 \
                        --nodes-max 3 \
                    '''
                }
            }
        }

        stage('Create config file cluster') {
            steps{
                withAWS(region:'us-west-2', credentials:'blueocean') {
                    sh '''
                        aws eks --region us-west-2 update-kubeconfig --name ekscluster
                    '''
                }
            }
        }
    }
}