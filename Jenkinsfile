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
       sh  "mvn clean sonar:sonar"
         }
   }
 stage('nexus'){
    steps{
       sh  "mvn clean deploy"
         }
   }
        // through tomcat server credentitals
        /*
   stage('deployTomcat'){
    steps{
deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://44.208.22.127:8080/')], contextPath: 'qenv', war: '**/*.war'
    }
   }
*/
//or deploy through the sshagent    
stage('Tomcat Deploy'){
            sshAgent[SSh]{
                sh "scp -o StrictHostKeyChecking=no target/vprofile-v2.war ubuntu@pubip:/opt/apache-tomcat-9.078/webapps"
            } 
        }
    }
}
