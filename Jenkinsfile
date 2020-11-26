node {
properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * *')])])
def mavenHome = tool name : "maven3.6.2" 

	
stage ("get code from git")
{
	git branch: 'development', url: 'https://github.com/sankeyx/maven-web-application.git'
}

stage ("build using maven")
{
sh "${mavenHome}/bin/mvn clean package" 	
}

stage ("deploy to tomcat server")
{  sshagent(['4d647e66-9336-4965-b9d3-111995bdf2fd']) { sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.127.242.168:/opt/apache-tomcat-9.0.39/webapps"
}
 	
}


}
