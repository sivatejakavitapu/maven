pipeline
{
   agent {label 'new'}
   stages
 {
     stage ('continous Download')
       {
          steps
           {
               git 'https://github.com/sivatejakavitapu/maven.git'
           }
       }
     stage ('continous build')
         { 
          steps
           {
                sh 'mvn package'
            }
         }
    stage ('continous deploy')
        {
        steps
            {
                deploy adapters: [tomcat9(credentialsId: '95eab3a0-0d96-4a28-a6e2-ee5259f4f079', path: '', url: 'http://172.31.3.160:8080')], contextPath: 'QA', war: '**/*.war'
            }
        }
        stage ('continous testing')
        {
            steps
            {
                git 'https://github.com/sivatejakavitapu/FunctionalTesting.git'
                sh 'java -jar /home/ubuntu/remote/workspace/Declarativepipeline/testing.jar'
            }
        }
         stage ('continous Delivery')
        {
        steps
            {
                deploy adapters: [tomcat9(credentialsId: '95eab3a0-0d96-4a28-a6e2-ee5259f4f079', path: '', url: 'http://172.31.14.153:8080')], contextPath: 'proddeploy', war: '**/*.war'
            }
        }
   }
} 
