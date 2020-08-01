node
{
    def mavenHome = tool name:"maven3.6.3"
    
    stage('SourceCodeManagement')
    {
      git branch: 'development', credentialsId: '29966239-6a1d-4283-8abe-ab0619405e67', url: 'https://github.com/SureshA3026/maven-web-application.git'  
    }
    stage('BulidArtifact')
{
    sh "${mavenHome}/bin/mvn clean package"
}
stage('SonarqubeReport')
{
    sh "${mavenHome}/bin/mvn clean sonar:sonar"
}
stage('UploadIntoNexus')
{
    sh "${mavenHome}/bin/mvn clean deploy"
}
stage('DeployIntoTomcat')
{
    sshagent(['f15a0f07-c36b-4df8-a781-7aafe01e759b'])
{
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@18.191.165.140:/opt/apache-tomcat-9.0.37/webapps/"
}
}
stage('EmailNotificaation')
{
 emailext body: 'Build is Done', subject: 'Build is Over', to: 'capt.sureshreddy@gmail.com'   
}
}
