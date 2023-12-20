pipeline
{
    agent any
    tools
    {
        maven "maven3.9.6"
    }
    stages
    {
        stage('checkfromgit')
        {
            steps{
                git credentialsId: 'c768473b-9c23-4732-ab76-debb6e16f054', url: 'https://github.com/DevOpsmkiran/maven-web-application.git'
            }
        }
        stage('BuildPackage')
        {
            steps{
                sh "mvn clean package"
            }
        }
        stage('Deploytoomcat')
        {
            steps{
                    sshagent(['b9c38086-73b4-46c4-99f6-ab89bf05f586']) 
                    {
                        sh "scp -o stricthostkeychecking=no target/maven-web-application.war ec2-user@43.204.233.177:/opt/apache-tomcat-9/webapps/"            
                    }
            }
        }
    }
}
