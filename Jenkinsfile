pipeline{
    agent any
    
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
                sh 'mvn clean sonar:sonar'
            }
        }
      
 stage('nexus'){
    steps{
       sh  "mvn clean deploy -DaltDeploymentRepository=your-repository-id::default::http://admin:admin@18.205.188.18:8081/repository/vprofile-app/"
         }
   }
        // through tomcat server credentitals
        
   stage('deployTomcat'){
    steps{
deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://3.87.209.44:8080/')], contextPath: 'vprofile', war: '**/*.war'
    }
   }
  /*
//or deploy through the sshagent    
stage('Tomcat Deploy'){
            sshAgent[SSh]{
                sh "scp -o StrictHostKeyChecking=no target/vprofile-v2.war ubuntu@3.87.209.44:/opt/apache-tomcat-9.078/webapps"
            } 
        }
        */
    }
}
