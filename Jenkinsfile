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
            sh 'sudo rm -r *;sudo git clone https://github.com/aleti-pavan/jenkins.git'
        }
    }
    stage('tfsvars create'){
        steps {
            sh 'sudo cp /home/ubuntu/lambda/vars.tf ./jenkins/'
        }
    }
    stage('terraform init') {
        steps {
            sh 'sudo /home/ubuntu/lambda/terraform init ./jenkins'
        }
    }
    stage('terraform plan') {
        steps {
            sh 'ls ./jenkins; sudo /home/ubuntu/lambda/terraform plan -target=resource.hello-world -var-file hello-world-poc.tfvars  -out hello-world-poc.tfplan ./jenkins'
        }
    }
	stage('terraform apply') {
        steps {
            sh 'sudo /home/ubuntu/lambda/terraform apply hello-world-poc.tfplan ./jenkins'
        }
    }
    stage('terraform ended') {
        steps {
            sh 'echo "Ended....!!"'
        }
    }

    
}
