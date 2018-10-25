pipeline { 
     agent { 
	node { 
	    label 'master' 
	   }
	 }

stages {

    stage('terraform started') {
        steps {
            sh 'echo "Started...!" '
        }
    }
    stage('git clone') {
        steps {
            sh 'sudo rm -r *;sudo git clone https://github.com/Anjan-Kumar/Demo.git'
        }
    }
    stage('tfsvars create'){
        steps {
            sh 'sudo cp /home/ubuntu/lambda/vars.tf ./Demo/'
        }
    }
    stage('terraform init') {
        steps {
            sh 'sudo /home/ubuntu/lambda/terraform init ./Demo'
        }
    }
    stage('terraform plan') {
        steps {
            sh 'ls ./Demo; sudo /home/ubuntu/lambda/terraform plan -target=resource.hello-world -var-file hello-world-poc.tfvars  -out hello-world-poc.tfplan ./Demo'
        }
    }
	stage('terraform apply') {
        steps {
            sh 'sudo /home/ubuntu/lambda/terraform apply hello-world-poc.tfplan ./Demo'
        }
    }
    stage('terraform ended') {
        steps {
            sh 'echo "Ended....!!"'
        }
    }

  }
}
