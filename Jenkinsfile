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
	success {
            script {
                currentBuild.result = 'SUCCESS'
            }
        }

        always {
            step([$class: 'Mailer',
                notifyEverystableBuild: true,
                recipients: "duvva.raghavendra@gmail.com",
                sendToIndividuals: true])
        }
        failure {
            script {
                currentBuild.result = 'FAILURE'
            }
        }

        always {
            step([$class: 'Mailer',
                notifyEveryUnstableBuild: true,
                recipients: "duvva.raghavendra@gmail.com",
                sendToIndividuals: true])
        }
    }
}
