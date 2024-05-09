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
                sh "scp -o StrictHostKeyChecking=no devops-ap/target/devops-app.war ec2-user@54.83.125.116:/opt/tomcat/webapps"
                // restart tomcat 
                sh "ssh ec2-user@54.83.125.116 /opt/tomcat/bin/shutdown.sh"
                sh "ssh ec2-user@54.83.125.116 /opt/tomcat/bin/startup.sh"
            }
              }
                }
    }
}
