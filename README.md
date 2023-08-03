# vprofile-project-ci-jenkins

 cd vprofile-project-ci-jenkins/
   #ls
   # in pom.xml check the credentails
    #vi pom.xml
![Screenshot (308)](https://github.com/bvenkydevops/vprofile-project-ci-jenkins/assets/104990262/4e79b161-456f-4a48-9ee7-44a39f729ae8)

   #mvn package
  #mvn deploy -DaltDeploymentRepository=repository-id::default::http://admin:admin@18.205.188.18:8081/repository/v-profile-release/
  ![Screenshot (309)](https://github.com/bvenkydevops/vprofile-project-ci-jenkins/assets/104990262/f830a2f4-cb0b-4efe-931c-cc8f2930583c)

# check the nexus repository
![Screenshot (307)](https://github.com/bvenkydevops/vprofile-project-ci-jenkins/assets/104990262/b09b8d08-be24-43f5-9e8d-8b357dfad568)

# after  deploy accessing the application through webbrowser https://publicip:8080

![v-profile](https://github.com/bvenkydevops/vprofile-project-ci-jenkins/assets/104990262/8e6b9e5a-13e3-4bac-8584-d51e25e6b8fa)

