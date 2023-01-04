node{
    
    def mavenHome = tool name: 'maven3.8.5'
    
    stage('checkoutfromGit')
    {
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
