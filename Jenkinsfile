node{
properties([pipelineTriggers([pollSCM('* * * * *')])])

def mavenHome = tool name: "maven3.6.3"
stage("getting code from scm")    
{
    git branch: 'development', url: 'https://github.com/sankeyx/maven-web-application.git'
}    
    
stage("build using maven")
{
sh "${mavenHome}/bin/mvn clean package"    
    
}
/*
stage("sonar scaner")  
{
    sh "${mavenHome}/bin/mvn sonar:sonar"
}
stage("upload artifact to nexus")  
{
    sh "${mavenHome}/bin/mvn deploy"
}
*/
stage("deploy to tomcat server")  
{
   sshagent(['a7d7dc38-552d-4925-a535-73d45116329d']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@65.1.111.121:/opt/tomcat/webapps/" 
}
} 
    
}
