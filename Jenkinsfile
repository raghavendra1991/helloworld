// Declarative pipeline
pipeline {
    agent any

    stages {

        stage ('Git Checkout') {
            steps {
                git branch:'master'
                    credentialsId:'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'
                    url:'ssh://git@github.com:raghavendra1991/helloworld.git'
                sh "ls -lat"
            }
        }
        stage('Compile Stage') {
            steps {
                sh "mvn clean compile"
            }
        }
        stage('Testing') {
            steps {
                sh "mvn test"
            }
        }
        stage('Package') {
            steps {
                sh "mvn package"
            }
        }
        stage('Deploy') {
            steps {
                sh "mvn tomcat:deploy"
            }
        }
    }
    post {
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
