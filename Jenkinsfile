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
            sh "mvn clean package"
            sh "mv target/*.war target/myweb.war"
             }
            }
     stage("deploy-dev"){
       steps{
          sshagent(['3.87.15.40']) {
          sh """
          scp -o StrictHostKeyChecking=no target/myweb.war  
          ubuntu@3.87.15.40:/opt/tomcat/webapps/
          ssh ubuntu@3.87.15.40 /opt/tomcat/bin/shutdown.sh
          ssh ubuntu@3.87.15.40 /opt/tomcat/bin/startup.sh
           """
            }
          }
        }
      }
    }
