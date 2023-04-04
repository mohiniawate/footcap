pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                // Build your application and create a Docker image
                sh 'docker build -t footcap-nginx .'
            }
        }
        stage('Push') {
            steps {
                // Push the Docker image to your ECR repository
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: "awscredit", secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                    sh 'aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/u4p8s1t2'
                    sh 'docker tag footcap-repo:latest public.ecr.aws/u4p8s1t2/footcap-repo:latest'
                    sh 'docker push public.ecr.aws/u4p8s1t2/footcap-repo:latest'
                }
            }
        }
        // stage('Deploy') {
        //     steps {
        //         // Deploy the Docker image to your ECS cluster and service
        //         ecsUpdateService(
        //             cluster: 'footcap-naginx',
        //             service: 'footcap-test-service',
        //             image: 'public.ecr.aws/n7a1b8r0/footcap-nginx:latest',
        //             region: 'eu-north-1',
        //             waitForServiceCapacity: true,
        //             taskDefinitionOverride: ''
        //         )
        //     }
        // }
    }
}
