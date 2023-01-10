

pipeline {
  agent { 
  label 'nodes'
  }
  environment {
   AWS_EC2_PRIVATE_KEY=credentials('ec2-private-key') 
  }
  
  stages {
    
    //Get the Code from GitHub Repo
    stage('CheckOutCode'){
      steps{
         git credentialsId: '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', url: 'https://github.com/rss-april/jekins-ansible-dynimc-inv.git'
      }
    }
     
    //Run the playbook
    stage('RunPlaybook') {
      steps {
        //List the dymaic inventory just for verification
        sh "ansible-inventory --graph -i inventory/aws_ec2.yaml"
        //Run playbook using dynamic inventory & limit exuection only fo tomcatservers.
        sh "ansible-playbook -i inventory/aws_ec2.yaml  playbooks/tomcat-setup.yaml -u ec2-user --private-key=$AWS_EC2_PRIVATE_KEY --limit tomcatservers --ssh-common-args='-o StrictHostKeyChecking=no'"
      }
    }
  
  }//stages closing
}//pipeline closing
