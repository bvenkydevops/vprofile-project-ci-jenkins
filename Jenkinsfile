pipeline{
    agent any
    tools {
  maven 'maven'
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
       stage('sonarQube'){
            steps{
                sh ''
            }
        }
        stage('Nexus Artifact'){
            steps{
                sh 'mvn clean deploy'
            }
        }
        stage('Tomcat Deploy'){
            sshAgent[SSh]{
                sh "scp -o StrictHostKeyChecking=no target/vprofile-v2.war ubuntu@pubip:/opt/apache-tomcat-9.078/webapps"
            } 
        }
    }
}
