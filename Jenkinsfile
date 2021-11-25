pipeline 
{
   agent any
   stages
   {
       stage('ContinuousDownload')
       {
         steps
         {
            script
            {
                try
                {
                   git 'https://github.com/gassama85/maven.git'
                }
                catch(Exception e1)
                {
                   mail bcc: '', body: 'jenkins was unable to download the codes for project1 into the git repository', cc: '', from: '', replyTo: '', subject: 'download fail', to: 'dev.team@gmail.com'
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
                   mail bcc: '', body: 'jenkins is unable to build project1 codes into an artifact', cc: '', from: '', replyTo: '', subject: 'build failed', to: 'dev.team2@gmail.com'
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
                     deploy adapters: [tomcat9(credentialsId: '91d3b313-48dd-43b1-ba3a-8a50aaf34b82', path: '', url: 'http://172.31.84.101:8080')], contextPath: 'testapp', war: '**/*.war'
                 }
                 catch(Exception e3)
                 {
                  mail bcc: '', body: 'jenkins is unable to deploy codes for project1 into tomcat of QAServer ', cc: '', from: '', replyTo: '', subject: 'deployment failed', to: 'middleware.team@gmail.com'
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
                     git 'https://github.com/selenium-saikrishna/FunctionalTesting.git'
                     sh 'java -jar /home/ubuntu/.jenkins/workspace/Declarative_Pipeline/testing.jar'
                 }
                 catch(Exception e4)
                 {
                   mail bcc: '', body: 'jenkins is unable to run the selenium automation tools  ', cc: '', from: '', replyTo: '', subject: 'testing failed', to: 'testing.team@gmail.com'
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
                     deploy adapters: [tomcat9(credentialsId: '91d3b313-48dd-43b1-ba3a-8a50aaf34b82', path: '', url: 'http://172.31.94.132:8080')], contextPath: 'prodapp', war: '**/*.war'
                 }
                 catch(Exception e5)
                 {
                     mail bcc: '', body: 'jenkins is unable to deploy artifact for project1 into tomcat9 of the prodserver  ', cc: '', from: '', replyTo: '', subject: 'delivery failed', to: 'delivery.team@gmail.com'
                     exit(1)
                 }
             }
             
         }
       }
   }
}
