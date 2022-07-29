pipeline
{
    agent any
    stages
    { 
       stage('ContinuosDownload')
       {
          steps
          {
              script
              {
                  try
                  {
                    git branch: 'main', url: 'https://github.com/sumanthintime/Jenkins.git'
                  }
                  catch(Exception e1)
                  {
                      mail bcc: '', body: 'Jenkins Admin team please look at the failure at continous Download', cc: '', from: '', replyTo: '', subject: 'Continous Download Failed', to: 'admin@intime.com'
                      exit(1)
                      
                  }
                }
            }
        }  
             
     
       stage('ContinuosBuild')
       {
          steps
          {
              script
              {
                 sh 'mvn package'
                }
          }
       }
      
      stage('ContinuosDeployment')
       {
          steps
          {
             sh 'scp /home/ubuntu/.jenkins/workspace/DeclarativePipeline/webapp/target/webapp.war ubuntu@172.31.81.177:/var/lib/tomcat9/webapps/testapp.war'
             
          }
        }
       stage('ContinuosTesting')
       {
          steps
          {
             git branch: 'main', url: 'https://github.com/sumanthintime/FunctionalTesting.git'
             sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline2/testing.jar'
             
          }
        }
        stage('ContinuosDelivery')
       {
          steps
          {
             sh 'scp /home/ubuntu/.jenkins/workspace/DeclarativePipeline/webapp/target/webapp.war ubuntu@172.31.80.15:/var/lib/tomcat9/webapps/testapp.war'
             
          }
        }
    }
}
