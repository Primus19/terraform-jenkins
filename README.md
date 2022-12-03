# terraform-jenkins
# Expectations

- Deploy a jenkins server on an EC2 instance
- The EC2 instance should be accessible via the internet on port 8080
- Only you should be able to access the EC2 instance via SSH
- Use Terraform for Infrastructure as Code

# How to accomplish this task with Terraform?
- Create the VPC
- Create the Internet Gateway and attach it to the VPC using a Route Table
- Create a Public Subnet and associate it with the Route Table
- Create a Security Group for the EC2 Instance
- Create a script to automate the installation of Jenkins on the EC2 Instance
- Create the EC2 Instance and attach an Elastic IP and Key Pair to it
- Verify that everything works

# Prerequisites
AWS CLI is installed and configured
Terraform is installed

# Run this to create the required folder structure:
mkdir -p terraform-jenkins/modules/{compute,security_group,vpc} && cd terraform-jenkins && touch main.tf outputs.tf secrets.tfvars && cd modules/compute && touch main.tf outputs.tf install_jenkins.sh && cd ../security_group && touch main.tf outputs.tf && cd ../vpc && touch main.tf outputs.tf

# Run this to create your Keys:
ssh-keygen -t rsa -b 4096 -m pem -f tutorial_kp && mv tutorial_kp.pub modules/compute/tutorial_kp.pub && mv tutorial_kp tutorial_kp.pem && chmod 400 tutorial_kp.pem

# Run this to SSH into EC2
ssh -i tutorial_kp.pem ubuntu@$(terraform output -raw jenkins_public_ip)

# Use this to get the jenkins Admin password
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
