node {
    def mvnHome = tool name : "maven3.9.3"
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * *')])])
    stage('Checkoutcode') {
        git branch: 'dev', credentialsId: 'a2473b31-65cb-4f4c-8231-f77a4469683e', url: 'https://github.com/ashishnanaware/maven-web-application.git'        
    }
    //build the source code 
    stage('Build') {
        sh "$mvnHome/bin/mvn clean package"
    }
    stage('DeployToTomcat') {
        sshagent(['4290e62f-594f-4ada-b0e7-a552d89f54bf']) {
            sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@15.206.81.231://opt/apache-tomcat-9.0.76/webapps/"  
        }
    }//stage end
}//node end
