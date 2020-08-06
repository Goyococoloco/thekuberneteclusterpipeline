pipeline {
    agent any
    stages {
        stage('Create kubernetes cluster') {
            steps {
                withAWS(region:'us-west-2', credentials:'ekszugang') {
                    sh '''
                        eksctl create cluster \
                        --name theekscluster \
                        --version 1.17 \
                        --region us-west-2 \
                        --nodegroup-name theeksnodes \
                        --node-type t2.small \
                        --nodes 2 \
                        --nodes-min 1 \
                        --nodes-max 3 \
                    '''
                }
            }
        }

        stage('Create config file cluster') {
            steps{
                withAWS(region:'us-west-2', credentials:'ekszugang') {
                    sh '''
                        aws eks --region us-west-2 update-kubeconfig --name theekscluster
                    '''
                }
            }
        }
    }
}
