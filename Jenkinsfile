pipeline {
    agent any

    environment {
        AWS_ACCES_KEY_ID = credentials('AWS_ACCES_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
    }

    stages {
        stage('Set Packer Path') {
            steps {
                script {
                    def packHome = tool name: 'Packer'
                    env.PATH = "${packHome}:${env.PATH}"
                }
                sh 'packer -version'
            }
        }
        stage('Build Nginx Image') {
            steps {
                sh "packer build \
                     -var aws_access_key=$AWS_ACCES_KEY_ID \
                     -var aws_secret_key=$AWS_SECRET_ACCESS_KEY \
                     packer-nginx.json"
            }
        }
    }
}