pipeline{

agent any

tools{
maven 'maven3.8.5'
}

//This stage will get the Source from the Github
stages{
stage('CheckOutCode'){
steps{
    slackNotifications('STARTED')
  git branch: 'development', credentialsId: '932a7806-d5a8-488f-a360-c9ef95e65cdd', url: 'https://github.com/DevOpsmkiran/maven-web-application.git'
}
}
//This stage will do the build
stage('Build'){
steps{
sh "mvn clean package"
}
}
//This Stage will be execute SonarQube Report
stage('ExecuteSonarQubeReport'){
steps{
sh "mvn clean sonar:sonar"
}
}
//This stage will Upload the Artifcats into Nexus Repos
stage('UploadArtifactIntoArtifactoryRepo'){
steps{
sh "mvn clean deploy"
}
}

//Deploy Application Into Tomcat Server
stage('DeployAppIntoTomcatServer')
{
steps{
      sshagent(['ca8d71e0-fff9-430e-b498-a6a95b21e64b']) {
            
            sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war  ec2-user@172.31.40.246:/opt/apache-tomcat-9.0.65/webapps/"
        }
  /*
    sshagent(['dc292b7a-3b39-4630-9fc3-1b806b54412c']) {
          sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war  ec2-user@172.31.7.80:/opt/apache-tomcat-9.0.65/webapps/"
     }
  */
}
}

}//stages closing

post {
  success {
    slackNotifications(currentBuild.result)
  }
  failure {
    slackNotifications(currentBuild.result)
  }
}

}//pipeline closing

//Code Snippet for sending slack notifications.

def slackNotifications(String buildStatus = 'STARTED') {
  // build status of null means successful
  buildStatus =  buildStatus ?: 'SUCCESS'
  
  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    colorName = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESS') {
    colorName = 'GREEN'
    colorCode = '#00FF00'
  } else {
    colorName = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications
  slackSend (color: colorCode, message: summary, channel: "#sco")
}


