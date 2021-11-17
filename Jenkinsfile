pipeline {
    agent any

    environment {
        PATH                 = "${env.PATH}:~/.local/bin/"
        LOCAL_AWS_ACCESS_ID  = credentials('aws-key-id')
        LOCAL_AWS_ACCESS_KEY = credentials('aws-key-secret')
    }

    stages {
        stage('Provision') {
            steps {
                sh 'ansible-galaxy install -r requirements.yml'
                sh '''
                  source ./terraform-env.shl
                  terraform init -input=false
                  terraform plan -out=tfplan -input=false
                  terraform apply -input=false tfplan
                '''
            }
        }
    }
}
