pipeline {
    agent any

    stages {
        stage('maven build') {
            steps {
               sh "mvn clean package"
    }
}
          stage('tomcat-deploy') {
              steps {
                   //  install ssh agent plugin
            sshagent(['tomcat']) {
                sh "scp -o StrictHostKeyChecking=no target/devops-ap.war ec2-user@172.31.16.64:/opt/tomcat/webapps"
                // restart tomcat 
                sh "ssh ec2-user@172.31.16.64 /opt/tomcat/bin/shutdown.sh"
                sh "ssh ec2-user@172.31.16.64 /opt/tomcat/bin/startup.sh"
            }
              }
                }
    }
}
