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
        // Web Application Undeploy Tomact
        stage('redeploy Stage') {
            steps {
                sh "mvn tomcat:redeploy"
            }
        }
        // Web Application Deploy Tomact
        stage('Deploy Stage') {
            steps {
                sh "mvn tomcat:deploy"
            }
        }
        // Web Application Undeploy Tomact
        stage('Undeploy Stage') {
            steps {
                sh "mvn tomcat:undeploy"
            }
        }
        // Web Application Redeploy Tomcat
        stage('Redeploy Stage') {
            steps {
                sh "mvn tomcat:redeploy"
            }
        }
    }
    post {
    success {
      sh "echo 'Send mail on success'"
      // mail to:"duvva.raghavendra@gmail.com", subject:"SUCCESS: ${currentBuild.fullDisplayName}", body: "Yay, we passed."
    }
    failure {
      sh "echo 'Send mail on failure'"
      // mail to:"duvva.raghavendra@gmail.com", subject:"FAILURE: ${currentBuild.fullDisplayName}", body: "Boo, we failed."
    }
  }
}
