pipeline{
    agent any 
    stages{
       
        stage('mvn build'){
            steps{
                echo "maven step in jenkins file"
            sh 'mvn clean package'
                sh 'mv target/*.war target/myapp.war'
            }
        }
         stage('deploy tomcat'){
             steps{
              sshagent(['tomcat8']) {
                        sh """
                        scp -o StrictHostKeyChecking=no target/myapp.war ubuntu@172.31.34.138:/opt/tomcat/webapps/
                        ssh ubuntu@172.31.34.138 /opt/tomcat/bin/shutdown.sh
                         ssh ubuntu@172.31.34.138 /opt/tomcat/bin/startup.sh
                        
                        """
              }  
            }    
           
        
         }
    }
}
