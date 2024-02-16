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

Click on Create Role

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/2.avif" width="1000" height="400">

Select entity type as AWS service

Use case as EC2 and click on Next.

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/3.avif" width="1000" height="400">

For permission policy select Administrator Access (Just for learning purpose), click Next.

Provide a Name for Role and click on Create role.

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/4.avif" width="1000" height="400">

Role is created.

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/5.avif" width="1000" height="400">

Now Attach this role to Ec2 instance that we created earlier, so we can provision cluster from that instance.

Go to EC2 Dashboard and select the instance.

Click on Actions –> Security –> Modify IAM role.

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/6.avif" width="1000" height="400">

Select the Role that created earlier and click on Update IAM role.

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/7.avif" width="1000" height="400">

Connect the instance to Mobaxtreme or Putty

# STEP 3: Cluster provision

Now clone this Repo.

    git clone https://github.com/tohidhanfi20/k8s-mario

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/8.avif" width="1000" height="400">    

change directory

    cd k8s-mario

Provide the executable permission to script.sh file, and run it.

    sudo chmod +x script.sh
    ./script.sh

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/9.avif" width="1000" height="400">

This script will install Terraform, AWS cli, Kubectl, Docker.

Check versions

    docker --version
    aws --version
    kubectl version --client
    terraform --version

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/10.avif" width="1000" height="400">

Now change directory into the EKS-TF

Run Terraform init

NOTE: Don’t forgot to change the s3 bucket name in the backend.tf file

    cd EKS-TF
    terraform init

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/11.avif" width="1000" height="400">

Now run terraform validate and terraform plan

    terraform validate
    terraform plan
    
<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/12.avif" width="1000" height="800">

Now Run terraform apply to provision cluster.

    terraform apply --auto-approve

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/13.avif" width="1000" height="400">

Completed in 10mins

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/14.avif" width="1000" height="400">

Update the Kubernetes configuration

Make sure change your desired region

    aws eks update-kubeconfig --name EKS_CLOUD --region ap-south-1

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/15.avif" width="1000" height="1000">    

Now change directory back to k8s-mario

    cd ..

Let’s apply the deployment and service    

# Deployment

    kubectl apply -f deployment.yaml
    
#to check the deployment

    kubectl get all

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/16.avif" width="2000" height="200">   

Now let’s apply the service

# Service

    kubectl apply -f service.yaml
    kubectl get all
    
<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/17.avif" width="1000" height="600">

Now let’s describe the service and copy the LoadBalancer Ingress

    kubectl describe service mario-service

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/18.avif" width="1000" height="400">    

Paste the ingress link in a browser and you will see the Mario game.

Let’s Go back to 1985 and play the game like children.

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/19.avif" width="1000" height="400">

This is official image by MR CLOUD BOOK

You can check in Docker-hub as well sevenajay/mario:latest

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/20.avif" width="1000" height="400">

# Destruction 

Let’s remove the service and deployment first

    kubectl get all
    kubectl delete service mario-service
    kubectl delete deployment mario-deployment

Let’s Destroy the cluster

    terraform destroy --auto-approve

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/21.avif" width="1000" height="400">    

After 10mins Resources that are provisioned will be removed.

<img src="https://github.com/tohidhanfi20/k8s-mario/blob/main/Screenshots/22.avif" width="1000" height="400">    

"Thank you for joining this nostalgic journey to the 90s! We hope you enjoyed rekindling your love for gaming with the deployment of the iconic Mario game on Kubernetes. Embracing the past while exploring new technologies is a true testament to the timeless allure of classic games. Until next time, keep gaming and reliving those fantastic memories! 👾🎮."
