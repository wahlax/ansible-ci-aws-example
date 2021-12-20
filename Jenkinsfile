pipeline {
    agent any

    environment {
        PATH                 = "${env.PATH}:~/.local/bin/"
        LOCAL_AWS_ACCESS_ID  = credentials('aws-key-id')
        LOCAL_AWS_ACCESS_KEY = credentials('aws-key-secret')
    }

    parameters {
        choice(name: 'TERRAFORM_ACTION', choices: ['APPLY','DESTROY'], description: 'What action should terraform perform?')
    }

    stages {
        stage('Apply') {
            when {
                expression { TERRAFORM_ACTION == 'APPLY' }
            }
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

        stage('Destroy') {
            when {
                expression { TERRAFORM_ACTION == 'DESTROY' }
            }
            steps {
                sh '''
                  source ./terraform-env.shl
                  terraform destroy --auto-approve
                '''
            }
        }
    }
}
