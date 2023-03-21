pipeline{

agent any
	environment {
            FILE="/opt/maven-9/webapps/maven-web-application.war"
    }

tools{
maven 'maven-3.8.6'

}

/*triggers{
pollSCM('* * * * *')
}
*/
/*options{
timestamps()
buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5'))
}
*/

stages{

  stage('CheckOutCode'){
    steps{
    	script
                {
                    try
                    {	    
    			git branch: 'master', credentialsId: '957b543e-6f77-4cef-9aec-82e9b0230975', url: 'https://github.com/vikashmuktha/maven-web-application-jayadeep.git'
		    }
		catch(Exception e1)
                    {
                       mail bcc: '', body: 'jenkins is unable to download the code', cc: 'mukthavikash@gmail.com', from: '', replyTo: '', subject: 'download failed', to: 'vikashprepararion@gmail.com'
                        exit(1)
                    }
                }
    	}
  }
  
  stage('Build'){
  steps{
  sh  "mvn clean package"
  }
  }
/*
 stage('ExecuteSonarQubeReport'){
  steps{
  sh  "mvn clean sonar:sonar"
  }
  }
  
  stage('UploadArtifactsIntoNexus'){
  steps{
  sh  "mvn clean deploy"
  }
  }
  
  stage('DeployAppIntoTomcat'){
  steps{
  sshagent(['bfe1b3c1-c29b-4a4d-b97a-c068b7748cd0']) {
   sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@35.154.190.162:/opt/apache-tomcat-9.0.50/webapps/"    
  }
  }
  }
  }//Stages Closing

post{

 success{
 emailext to: 'devopstrainingblr@gmail.com,mithuntechnologies@yahoo.com',
          subject: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          body: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          replyTo: 'devopstrainingblr@gmail.com'
 }
 
 failure{
 emailext to: 'devopstrainingblr@gmail.com,mithuntechnologies@yahoo.com',
          subject: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          body: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          replyTo: 'devopstrainingblr@gmail.com'
 */
stage('file check'){
            steps{
                sshagent(['599ff7ef-ccdd-4438-bfdc-7a604ef587c1']) {
                    sh """ 
                    ssh ec2-user@172.31.49.183  "cd /opt/maven-9/webapps;  
                      if [ -f "$FILE" ];
                    then
                      echo "$FILE is exist"
                      	 "rm -rf cd /opt/maven-9/webapps/maven-web-application.war"
                    else
                       echo "$FILE is not exist"
                     fi  
                       "
                      """
                 }        
            }
        }	
/*stage('DeploytoContainer'){
            steps{
                sshagent(['599ff7ef-ccdd-4438-bfdc-7a604ef587c1']) {
                    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.49.183:/opt/maven-9/webapps/"
                }    
            }
        }
*/
 }
}

