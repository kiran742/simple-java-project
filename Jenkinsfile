pipeline{
    agent any 
    stages{
        stage('Git checkout'){
            steps{
              git credentialsId: 'githud_cred', url: 'https://github.com/kiran742/my-app.git'
            }
        }
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
                        ssh ubuntu@172.31.34.138 /opt/tomcat/shutdown.sh
                         ssh ubuntu@172.31.34.138 /opt/tomcat/startup.sh
                        
                        """
              }  
            }    
           
        
         }
    }
}
