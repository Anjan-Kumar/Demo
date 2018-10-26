pipeline {
     agent {
        node {
            label 'master'
           }
         }
/*
environment {
        AWS_ACCESS_KEY_ID     = credentials('aws_access_key')
        AWS_SECRET_ACCESS_KEY = credentials('aws_secret_key')
    }
*/

stages {

    stage('Pre Build') {
        steps {
            sh 'echo "Started...!" '
            echo sh(script: 'env|sort', returnStdout: true)
        }
    }
    stage('Terraform Deployment') {
        steps {
            withCredentials([
                usernamePassword(credentialsId: 'Anjan-AWS', passwordVariable: 'AWS_SECRET', usernameVariable: 'AWS_KEY'),
            ]) {

            }
            sh '''
                terraform init
                terraform plan -target=aws_lambda_function.demo_lambda -out demo_lambda.tfplan
                terraform apply demo_lambda.tfplan
            '''
        }
    }
    stage('Deployment Done') {
        steps {
            sh 'echo "Success....!!"'
        }
    }
  }
}



