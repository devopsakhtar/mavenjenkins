pipeline{
  agent any
  stages{
    stage("Git Checkout"){
      steps{
            git url: 'https://github.com/devopsakhtar/mavenjenkins.git'
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
          sshagent(['tomcat-dev1']) {
          sh """
          scp -o StrictHostKeyChecking=no target/myweb.war  
          ubuntu@172.31.7.215:/opt/tomcat/webapps/
          ssh ubuntu@172.31.7.215 /opt/tomcat/bin/shutdown.sh
          ssh ubuntu@172.31.7.215 /opt/tomcat/bin/startup.sh
           """
            }
          }
        }
      }
    }
