node{

def mavenHome = tool name: "maven3.8.6"
/*
echo "Jenkins url is: ${env.JENKINS_URL}"
echo "Node Name is: ${env.NODE_NAME}"
echo "Job name is: ${env.JOB_NAME}"
*/


stage('CheckOutCode'){
git branch: 'development', credentialsId: '166c70a2-1df5-4993-a566-0a795862da8c', url: 'https://github.com/MithunTechnologiesDevOps/maven-web-application.git'
}

stage('Build'){
sh "${mavenHome}/bin/mvn clean package"
}

/*
stage('ExecuteSonarQubeReport'){
sh "${mavenHome}/bin/mvn clean sonar:sonar"
}

stage('UploadArtifcatsIntoArtifactoryRepo'){
sh "${mavenHome}/bin/mvn clean deploy"
}

stage('DeployAppIntoTomcatServer'){
sshagent(['dc292b7a-3b39-4630-9fc3-1b806b54412c']) {
 sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war  ec2-user@172.31.7.80:/opt/apache-tomcat-9.0.65/webapps/"
}
}

}//Node closing
