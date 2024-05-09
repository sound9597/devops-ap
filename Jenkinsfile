pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sound9597/devops-ap.git'
               
            }
        }
        stage('maven build') {
            steps {
               sh "mvn clean package"
    }
}
          stage('tomcat-deploy') {
              steps {
                   //  install ssh agent plugin
            sshagent(['tomcat']) {
                sh "scp -o StrictHostKeyChecking=no /home/ec2-user/devops-app/target/devops-app.war ec2-user@54.83.125.116:/opt/tomcat/webapps"
                // restart tomcat 
                sh "ssh ec2-user@54.83.125.116 /opt/tomcat/bin/shutdown.sh"
                sh "ssh ec2-user@54.83.125.116 /opt/tomcat/bin/startup.sh"
            }
              }
                }
    }
