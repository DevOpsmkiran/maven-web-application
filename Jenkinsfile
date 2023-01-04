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





---------------------
node{

    
    def mavenHome = tool name: 'maven3.8.5'
    

//Checkout Code State
stage('CheckoutCode'){


}

//Build
stage('Build'){
sh "${mavenHome}/bin/mvn clean package"
}

 /*
//Execute SonarQube Report
stage('ExecuteSonarQubeReport'){
sh "${mavenHome}/bin/mvn sonar:sonar"
}

//UploadArtifcats Into Nexus
stage('UploadArtifcatsIntoNexus'){
sh "${mavenHome}/bin/mvn deploy"
}

//Deploy App into Tomcat Server
stage('DeployApp'){
sshagent(['e83477fc-0cee-45ee-a412-92e2240a7256']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.40.1:/opt/apache-tomcat-9.0.68/webapps/"
}
}

}//node closing


