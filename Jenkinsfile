node {
    
   properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '')), pipelineTriggers([pollSCM('* * * * *')])])
    //This is first my stage
    stage('GitCheckout'){
       git branch: 'development', url: 'https://github.com/manasareddy891/maven-web-application.git' 
    }
    
    stage('buildmavenproject'){
    
      sh '/var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven_3.6.3/bin/mvn clean install'  
    }
    
    stage('deployartifactsinto Nexus repo'){
        
        sh '/var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven_3.6.3/bin/mvn clean deploy'  
    }
    stage('deploytotomcat') {
    
      sshagent (credentials: ['tomcatec2-userprivatekey']) {
        sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.129.58.78:/opt/tomcat9/webapps"
      }
    }
    
    
}
