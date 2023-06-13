pipeline{
    agent any
    tools {
        maven 'maven3.9.2'
    }
    environment {
    AWS_ACCESS_KEY_ID = credentials('access-key')
    AWS_SECRET_ACCESS_KEY = credentials('secret-key')
    AWS_DEFAULT_REGION = 'us-east-1'
       
  }
    stages{
        stage('checkout'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/bvenkydevops/vprofile-project-ci-jenkins.git']])
            }
        }
        stage('build'){
            steps{
                sh 'mvn clean package'
            }
        }
       
        stage('deploy'){
            steps{
                sh 'mvn clean deploy'
            }
        }
        stage('sns-notifcation'){
            steps{
                script{
                //Configuring AWS credentials
           withCredentials([string(credentialsId: 'access-key', variable: 'access-key'), string(credentialsId: 'secret-key', variable: 'secret-key')]) {
               sh 'aws configure set aws_access_key_id access-key'
               sh 'aws configure set aws_secret_access_key secret-key'
               sh 'aws configure set default.region us-east-1' 
                }
                snsPublish(topicArn: 'arn:aws:sns:us-east-1:323578407133:sai-sns', message: 'Hello this is sai kumar!')
                }
            }
        }
        
        post{

 success{
 emailext to: 'venkatesh.marolix@gmail.com,venkatesh-workshop',
          subject: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          body: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          replyTo: 'devopstrainingblr@gmail.com'
 }
 
 failure{
 emailext to: 'venkatesh.marolix@gmail.com,venkatesh-workshop',
          subject: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          body: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          replyTo: 'devopstrainingblr@gmail.com'
 }
                
            }
        }
    }
}
