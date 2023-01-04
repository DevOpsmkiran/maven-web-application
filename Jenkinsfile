node{
    
    def mavenHome = tool name: 'maven3.8.5'
    
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
    
    stage('checkoutfromGit')
    {
        sendSlackNotifications('STARTED')
        git branch: 'development', credentialsId: '932a7806-d5a8-488f-a360-c9ef95e65cdd', url: 'https://github.com/DevOpsmkiran/maven-web-application.git'
    }
    
    stage('BuildProject')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('ExecuteSonarQubeReport')
    {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    
    stage('UploadArtifacttoNexus')
    {
        sh "${mavenHome}/bin/mvn deploy"
    }
    
    stage('DeploytoTomcat')
    {
        sshagent(['d4d065cc-71b2-4814-8576-dfdffeaeb0ee']) 
        {
            sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.40.246:/opt/apache-tomcat-9.0.68/webapps"
        }
    }

}

def sendSlackNotifications(String buildStatus = 'STARTED') {
  
  buildStatus =  buildStatus ?: 'SUCCESS'

  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    color = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESS') {
    color = 'GREEN'
    colorCode = '#00FF00'
  } else {
    color = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications
  slackSend (color: colorCode, message: summary, channel: '#soc')
}

