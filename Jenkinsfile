pipeline{
    agent any
    tools{
        maven 'billionaire'
    }
    stages{
        stage("Clone Code from Github"){
            steps{
                script{
                    git branch: 'master', url: 'https://github.com/473tech/maven-web-application.git'
                }
            }
        }

        stage("Maven Test"){
            steps{
                script{
                    sh "mvn clean test"
                }
            }
        }
        stage("Maven Install"){
            steps{
                script{
                    sh "mvn clean install"
                }
            }
        }

        stage("Sonarqube Code Quality"){
            steps{
                script{
                    sh "mvn sonar:sonar"
                }
            }
        }

        stage("Nexus Artifact Stage"){
            steps{
                script{
                    sh "mvn deploy"
                }
            }
        }

        stage("Deploy to TOMCAT"){
            steps{
                script{
                    deploy adapters: [tomcat9(credentialsId: 'tomcatId', path: '', url: 'http://3.82.113.67:8080')], contextPath: null, war: 'target/*.war'
                }
            }
        }
    }

   post{
    always{
        sh "echo the build ran"
        mail bcc: '', body: 'Some just did a build', cc: '', from: '', replyTo: '', subject: 'Love and light from here', to: 'tolux17@gmail.com'
    }
    success{
        sh "echo the build ran successfully"
        mail bcc: '', body: 'Build success', cc: '', from: '', replyTo: '', subject: 'Love and light from here', to: 'tolux17@gmail.com'
    }
    failure{
        sh "echo the build failed woefully"
        mail bcc: '', body: 'Build failure', cc: '', from: '', replyTo: '', subject: 'Love and light from here', to: 'tolux17@gmail.com'
    }
   }
}
