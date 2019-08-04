node('master')
{
    stage('continuous download')
    {
        git 'https://github.com/katakamlokesh/maven.git'
    }
    stage('continuous build')
    {
        sh label: '', script: 'mvn package'
    }
   
    stage (' continuous deploy')
    {
       sh label: '', script: '''scp /home/ubuntu/.jenkins/workspace/Scripted_pipeline/webapp/target/webapp.war ubuntu@172.31.47.254:/var/lib/tomcat8/webapps/testenv.war'''
    }
    stage('continuous testing')
    {
        git 'https://github.com/katakamlokesh/FunctionalTesting.git'
        sh label: '', script: 'java -jar /home/ubuntu/.jenkins/workspace/Scripted_pipeline/testing.jar'
    }
     
    stage (' continuous delivery')
    {
         input message: 'waiting approval from DM ', submitter: 'Srinivas'
         sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/Scripted_pipeline/webapp/target/webapp.war ubuntu@172.31.40.241:/var/lib/tomcat8/webapps/prodenv.war'
    }
}
