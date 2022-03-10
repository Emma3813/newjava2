
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
                      git 'https://github.com/intelliqittrainings/maven.git'  
                    }
                      catch(Exception e1)
                    {
                    mail bcc: '', body: 'jenkins is unable to download the development code from the remote github', cc: '', from: '', replyTo: '', subject: 'download failed', to: 'git.emma@gmail.com'    
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
                      mail bcc: '', body: 'jenkins is unable to crate an artifact from the code ', cc: '', from: '', replyTo: '', subject: 'build failed', to: 'dev.team@gmail.com'
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
                       deploy adapters: [tomcat9(credentialsId: 'b7afcd11-dc4e-4f4e-a8af-990bd5353677', path: '', url: 'http://172.31.20.107:8080')], contextPath: 'test1', war: '**/*.war' 
                    }
                    catch(Exception e3)
                    {
                     mail bcc: '', body: 'jenkins is unable to deploy to the tomcat on prodserver', cc: '', from: '', replyTo: '', subject: 'deployment failed', to: 'middlewear.team@gmail.com'
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
              sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline/testing.jar'    
                    }
                    catch(Exception e4)
                    {
                      mail bcc: '', body: 'selenium test script are giving failure status', cc: '', from: '', replyTo: '', subject: 'testing failed', to: 'prod.team@gmail.com'
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
                      deploy adapters: [tomcat9(credentialsId: 'b7afcd11-dc4e-4f4e-a8af-990bd5353677', path: '', url: 'http://172.31.29.136:8080')], contextPath: 'testapp', war: '**/*.war'  
                    }
                    catch(Exception e5)
                    {
                      mail bcc: '', body: 'jenkins is unable to deploy into tomcat on the qa server', cc: '', from: '', replyTo: '', subject: 'delivery failed', to: 'delivery.team@gmail.com'
                      exit(1)
                    }
                }
              
            }
        }
        
    }
}

