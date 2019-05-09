pipeline {
    agent any

    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn test'
                }
            }
        }


        stage ('install Stage') {
            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn install'
                }
            }
        }

//node{
//  stage('SCM Checkout'){
//     git 'https://github.com/prakashk0301/jenkins-example'
//  }
//   stage('Compile-Package'){
//      // Get maven home path
//      def mvnHome =  tool name: 'localMaven', type: 'maven'   
//      sh "${mvnHome}/bin/mvn package"
//   }
   stage('Deploy to Tomcat'){
      
      sshagent(['deploy-dev']) {
         sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.42.125:/var/lib/tomcat/webapps/'
      }
   }
}
