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
        
        
        stage ('deploy Stage') {
            {sshagent(['deploy-dev']) {
                    sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.42.125:/var/lib/tomcat/webapps/'
            }
               }
            }
        }
    }

