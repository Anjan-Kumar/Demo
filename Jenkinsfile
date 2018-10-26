pipeline {
     agent {
        node {
            label 'master'
           }
         }

environment {
        AWS_ACCESS_KEY_ID     = credentials('jenkins-aws-secret-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('jenkins-aws-secret-access-key')
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
            sh 'terraform plan -target=aws_lambda_function.demo_lambda -out demo_lambda.tfplan'
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


