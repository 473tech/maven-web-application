pipeline{
    agent any
    tools{
        maven "maven-3.9.4"
    }
    stages{
        stage("Git Clone"){
            steps{
                echo "Cloning the code from Github"
                git 'https://github.com/473tech/maven-web-application.git'
            }
        }

       stage("Maven Test"){
        steps{
            sh "mvn clean test"
         }
       }

       stage("Maven Package"){
        steps{
            sh "mvn clean package"
         }
       }
       stage("Sonar Code quality"){
        steps{
            sh "mvn sonar:sonar"
        }
       }

       stage("Maven to Nexus"){
        steps{
            sh "mvn deploy"
        }
       }

       stage("Deploy to UAT"){
        steps{
            mail bcc: '', body: 'AHAHAHAHAHAH', cc: '', from: '', replyTo: '', subject: 'We deployed to your Environment, Please review within 48 hours', to: 'tolux17@gmail.com'
            deploy adapters: [tomcat9(credentialsId: 'tomcatId', path: '', url: 'http://54.227.227.122:8080')], contextPath: null, war: 'target/*.war'
             }
       }

       stage("Review"){
        steps{
            timeout(time: 120, unit: 'SECONDS') {
                 input 'Please review to proceed'
                }
           
        }
       }

       stage("Deploy to Production"){
        steps{
            deploy adapters: [tomcat9(credentialsId: 'tomcatId', path: '', url: 'http://54.227.227.122:8080')], contextPath: null, war: 'target/*.war'
             }
       }
    }

    post{
        always{
            echo "The build ran"
        }
        success{
            echo "The build succeeded"
        }
        failure{
            echo "The build failed"
        }
    }
}
