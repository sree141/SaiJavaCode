pipeline{
  agent any
  stages{
    stage("Git Checkout"){
      steps{
            git credentialsId: 'github', url: 'https://github.com/sree141/SaiJavaCode.git'
           }
          }
     stage("Maven Build"){
       steps{
            sh "/opt/apache-maven-3.8.3/bin/mvn package"
             }
            }
     stage("deploy-dev"){
       steps{
          sshagent(['3.82.186.105'])  {
          sh """
          scp -o StrictHostKeyChecking=no target/webapp.war ubuntu@3.82.186.105:/opt/tomcat/webapps/
          ssh ubuntu@3.82.186.105 /opt/tomcat/bin/shutdown.sh
          ssh ubuntu@3.82.186.105 /opt/tomcat/bin/startup.sh
           """
            }
          }
        }
      }
    }
