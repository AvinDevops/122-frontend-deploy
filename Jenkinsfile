pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time:30, unit:'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    parameters {
        string(name: 'appVersion', defaultValue: '1.1.0', description: 'What is the application version?')
    }
    environment {
        def appVersion = ''
    }
    stages {
        stage('print version') {
            steps {
                script {
                    echo "application version is : ${params.appVersion}"
                }
                
            }
        }
        stage('Init') {
            steps {
                sh """
                    cd terraform
                    terraform init
                """
            }
        }
        stage('Plan') {
            steps {
                sh """
                    cd terraform
                    terraform plan -var="app_version=${params.appVersion}"
                """
            }
        }
        stage('Deploy') {
            steps {
                sh """
                    cd terraform
                    terraform apply -auto-approve -var="app_version=${params.appVersion}"
                """
            }
        }
        
    }
    post {
        always {
            echo "this will run always"
            deleteDir()
        }
        success {
            echo "this will run when pipeline is success"
        }
        failure {
            echo "this will run when pipeline is failed"
        }
    }
}