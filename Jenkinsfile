// Declarative pipeline
pipeline {
    agent any
    tools {
        maven 'M2_HOME'
        jdk 'JAVA_HOME'
    }
    stages {
        // Static Code Analysis
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
        // Web Application Build
        stage('Build Stage') {
            steps {
                sh "mvn clean compile"
            }
        }
        // Web Apllication Unit Test
        stage('Testing Stage') {
            steps {
                sh "mvn test"
            }
        }
        // Web Application Packaging
        stage('Package Stage') {
            steps {
                sh "mvn package"
            }
        }
        // Web Application Deploy Tomact
        stage('Deploy Stage') {
            steps {
                sh "mvn tomcat:redeploy"
                sh "mvn tomcat:undeploy"
                sh "mvn tomcat:deploy"
            }
        }
    }

post {  
         always {  
             echo 'This will always run'  
         }  
         success {  
             echo 'This will run only if successful'
             mail bcc: '', body: "<b>Example</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "SUCCESS CI: Project name -> ${env.JOB_NAME}", to: "duvva.raghavendra@gmail.com";  
         }  
         failure {  
             mail bcc: '', body: "<b>Example</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: "duvva.raghavendra@gmail.com";  
         }  
         unstable {  
             echo 'This will run only if the run was marked as unstable'  
         }  
         changed {  
             echo 'This will run only if the state of the Pipeline has changed'  
             echo 'For example, if the Pipeline was previously failing but is now successful'  
         }  
     }
}
