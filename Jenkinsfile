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
                usernamePassword(credentialsId: 'ada90a34-30ef-47fb-8a7f-a97fe69ff93f', passwordVariable: 'AWS_SECRET', usernameVariable: 'AWS_KEY'),
                usernamePassword(credentialsId: '2facaea2-613b-4f34-9fb7-1dc2daf25c45', passwordVariable: 'REPO_PASS', usernameVariable: 'REPO_USER'),
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



