node
{

def mavenHome = tool name: "maven3.6.2"

 stage('CheckoutCode')
 {
  git branch: 'development', credentialsId: '0eb44278-575c-4a51-bd77-a797d525e698', url: 'https://github.com/MithunTechnologiesDevOps/maven-web-application.git'
 }
 
 stage('Build')
 {
 
 sh "${mavenHome}/bin/mvn clean package"
 }
 /*
 stage('ExecuteSonarQubeReport')
 {
 sh "${mavenHome}/bin/mvn sonar:sonar"
 }
 
stage('UploadArtifactIntoNexus')
 {
 sh "${mavenHome}/bin/mvn deploy"
 }
 
 stage('DeployAppIntoTomcat')
 {
 sshagent(['75e008d7-07fd-4b6f-a304-8ebf001de700']) 
 {
  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war  ec2-user@18.188.246.142:/opt/apache-tomcat-9.0.39/webapps/"   
 }
 }
 
 stage('SendEmailNotiifcation')
 {
 mail bcc: '', body: '''Build Over..

 Regards,
 Mithun Technologies,
 9980923226.''', cc: 'bhaskar0504@gmail.com', from: '', replyTo: '', subject: 'Build Over', to: 'devopstrainingblr@gmail.com'
 }

 */
 
}
