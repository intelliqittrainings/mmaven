pipeline
{
    agent any
    stages
    {
        stage('ContnuousDownload')
        {
            steps
            {
                script
                {
                  try
                  {
                    git 'https://github.com/intelliqittrainings/mmaven.git'
                  }
                  catch(Exception e1)
                  {
                     mail bcc: '', body: 'Jenkins is ub=nable to download the dev code form the git repo', cc: '', from: '', replyTo: '', subject: 'Download failed', to: 'git.admin@gmail.com'
                    exit(1)
                  }
                 
                }
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                script
                {
                try
                {
                     sh 'mvn package'
                }
                catch(Exception e2)
                {
                    mail bcc: '', body: 'Jenkins is unable to build an artifact from the code', cc: '', from: '', replyTo: '', subject: 'Build failed', to: 'developers@gmail.com'
                    exit(1)
                }
                }
               
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                script
                {
                    
                
                try
                {
                    sh 'scp /home/ubuntu/.jenkins/workspace/DeclarativePipeline2/webapp/target/webapp.war ubuntu@172.31.21.238:/var/lib/tomcat9/webapps/qaapp.war'
                }
                catch(Exception e3)
                {
                    mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on the QAServer', cc: '', from: '', replyTo: '', subject: 'Deployment failed', to: 'middleware.team@gmail.com'
                    exit(1)
                }
                }
                
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
             script
             {
                try
                {
                    git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline2/testing.jar'
                }
                catch(Exception e4)
                {
                    mail bcc: '', body: 'Functional testing has failed', cc: '', from: '', replyTo: '', subject: 'Testing failed', to: 'qa.team@gmail.com'
                    exit(1)
                }
             }
                
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                script
                {
                try
                {
                    sh 'scp /home/ubuntu/.jenkins/workspace/DeclarativePipeline2/webapp/target/webapp.war ubuntu@172.31.23.131:/var/lib/tomcat9/webapps/prodapp.war' 
                }
                catch(Exception e5)
                {
                    mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on the prodservers', cc: '', from: '', replyTo: '', subject: 'Delivery failed', to: 'delivery.team@gmail.com'
                }
                }
                
            }
        }
       
    }
}
