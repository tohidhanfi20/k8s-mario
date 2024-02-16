# k8s-mario
<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/Deploy-Super-Mario-Game-on-AWS-EKS.png" width="1000" height="400">

"Hey folks, remember the thrill of 90's gaming? Let's step back
in time and relive those exciting moments! With the game deployed on
Kubernetes, it's time to dive into the nostalgic world of Mario. Grab
your controllers, it's game time!"

# Introduction
Super Mario is a classic game loved by many. In this guide, we’ll explore how to deploy a Super Mario game on Amazon’s Elastic Kubernetes Service (EKS). Utilizing Kubernetes, we can orchestrate the game’s deployment on AWS EKS, allowing for scalability, reliability, and easy management.

# Prerequisites:
1) An Ubuntu Instance
2) IAM role
3) Terraform should be installed on instance
4) AWS CLI and KUBECTL on Instance

# LET’S DEPLOY

# STEP 1: Launch Ubuntu instance

1) Sign in to AWS Console: Log in to your AWS Management Console.
2) Navigate to EC2 Dashboard: Go to the EC2 Dashboard by selecting “Services” in the top menu and then choosing “EC2” under the Compute section.
3) Launch Instance: Click on the “Launch Instance” button to start the instance creation process.
4) Choose an Amazon Machine Image (AMI): Select an appropriate AMI for your instance. For example, you can choose Ubuntu image.
5) Choose an Instance Type: In the “Choose Instance Type” step, select t2.micro as your instance type. Proceed by clicking “Next: Configure Instance Details.”
6) Configure Instance Details:
   For “Number of Instances,” set it to 1 (unless you need multiple instances).
   Configure additional settings like network, subnets, IAM role, etc., if necessary.
   For “Storage,” click “Add New Volume” and set the size to 8GB (or modify the existing storage to 8GB).
   Click “Next: Add Tags” when you’re done.
7) Add Tags (Optional): Add any desired tags to your instance. This step is optional, but it helps in organizing instances.
8) Configure Security Group:
   Choose an existing security group or create a new one.
   Ensure the security group has the necessary inbound/outbound rules to allow access as required.
9) Review and Launch: Review the configuration details. Ensure everything is set as desired.
10) Select Key Pair:
   Select “Choose an existing key pair” and choose the key pair from the dropdown.
   Acknowledge that you have access to the selected private key file.
   Click “Launch Instances” to create the instance.
11) Access the EC2 Instance: Once the instance is launched, you can access it using the key pair and the instance’s public IP or DNS.

Ensure you have necessary permissions and follow best practices while configuring security groups and key pairs to maintain security for your EC2 instance.

# STEP 2: Create IAM role

Search for IAM in the search bar of AWS and click on roles.

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/d4f64b19-c42e-46ca-b2a5-470976c4403e.avif" width="1000" height="400">
