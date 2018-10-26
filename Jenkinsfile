pipeline {
     agent {
        node {
            label 'master'
           }
         }

stages {

    stage('Pre Build') {
        steps {
            sh 'echo "Started...!" '
            echo sh(script: 'env|sort', returnStdout: true)
        }
    }
    stage('Terraform Init') {
        steps {
            sh 'terraform init'
        }
    }
    stage('Terraform Plan') {
        steps {
            sh 'terraform plan -target=aws_lambda_function.demo_lambda -var-file terraform.tfvars -out demo_lambda.tfplan'
        }
    }
        stage('Terraform Apply') {
        steps {
            sh 'terraform apply demo_lambda.tfplan'
        }
    }
    stage('Deployment Done') {
        steps {
            sh 'echo "Success....!!"'
        }
    }
  }
}


