# AWS Infrastructure Automation Using Terraform

## Project Overview

This project demonstrates how to automate AWS infrastructure provisioning using Terraform.

It creates a VPC with two public subnets across different Availability Zones, deploys two EC2 instances running Apache web servers, creates an S3 bucket, and configures an Application Load Balancer (ALB) to distribute incoming HTTP traffic between the web servers.

The goal is to understand Infrastructure as Code (IaC), AWS networking, web server deployment, and load balancing.

## Architecture

```text
                       Users
                         |
                         v
                      Internet
                         |
                         v
              Application Load Balancer
                         |
                         v
                    Target Group
                    /           \
                   v             v
              EC2 Server 1   EC2 Server 2
                 Apache         Apache
                   |             |
               Subnet 1       Subnet 2
                   \             /
                    \           /
                        VPC

                   Amazon S3
               Object Storage
```

Note: The S3 bucket is created separately. Uploading files to S3 and integrating them with the EC2 instances requires additional configuration.

## AWS Services Used

### 1. Amazon VPC
Creates a logically isolated network for the project resources.

### 2. Subnets
Creates two subnets in different Availability Zones within the Stockholm Region.

### 3. Internet Gateway
Provides an internet route for appropriately configured resources in the VPC.

### 4. Route Table
Directs internet-bound traffic through the Internet Gateway.

### 5. Security Groups
Controls inbound and outbound network traffic for the AWS resources.

### 6. Amazon EC2
Launches two virtual servers to host web applications using Apache.

### 7. User Data
Installs Apache and creates the website HTML files when the EC2 instances initially launch.

### 8. Amazon S3
Creates an object storage bucket for storing files, images, backups, and application artifacts.

### 9. Application Load Balancer
Provides a single entry point for HTTP traffic and distributes requests across registered backend instances.

### 10. Target Group
Registers the EC2 instances and performs health checks to determine whether they can receive traffic.

### 11. ALB Listener
Listens for HTTP requests on port 80 and forwards them to the target group.

### 12. Terraform
Automates infrastructure provisioning and management through configuration files.

## Project Features

- Infrastructure as Code using Terraform
- Custom VPC and subnet configuration
- Two EC2 web servers
- Apache installation using user-data scripts
- Internet Gateway and route table configuration
- Security group configuration
- Amazon S3 bucket creation
- Application Load Balancer configuration
- Target group registration and health checks
- Terraform outputs for retrieving the ALB DNS name

## Project Structure

```text
TerraformVAC/
├── main.tf
├── provider.tf
├── variables.tf
├── userdata.sh
├── userdata1.sh
├── README.md
└── .gitignore
```

## Prerequisites

Before deploying this project, make sure you have:

- An AWS account
- Terraform installed
- AWS CLI installed and configured
- Git installed
- An Ubuntu AMI available in the eu-north-1 Region
- Appropriate AWS IAM permissions to create the required resources

## AWS Region

The project uses:

```text
eu-north-1
```

This is the Europe (Stockholm) AWS Region.

## Deployment Steps

### Step 1: Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/terraform-aws-alb-project.git
```

Replace `YOUR_USERNAME` with your GitHub username.

### Step 2: Enter the Project Directory

```bash
cd terraform-aws-alb-project
```

### Step 3: Configure AWS Credentials

Configure the AWS CLI using an appropriate authentication method.

```bash
aws configure
```

Do not commit AWS access keys or secret credentials to GitHub.

### Step 4: Review the Configuration

Check the Terraform files and confirm that:

- The AMI ID is valid in the selected AWS Region.
- The S3 bucket name is globally unique.
- The SSH security group rule uses your current public IP address.
- The Terraform variables are configured correctly.

### Step 5: Initialize Terraform

```bash
terraform init
```

### Step 6: Format and Validate

```bash
terraform fmt
terraform validate
```

### Step 7: Review the Execution Plan

```bash
terraform plan
```

Review the planned changes before creating resources.

### Step 8: Deploy the Infrastructure

```bash
terraform apply
```

Review the plan and type `yes` when Terraform requests confirmation.

### Step 9: Retrieve the ALB DNS Name

```bash
terraform output -raw loadbalancerdns
```

Open the resulting DNS name in your browser using HTTP:

```text
http://YOUR_ALB_DNS_NAME
```

Replace `YOUR_ALB_DNS_NAME` with the DNS name returned by Terraform.

## Verification

After deployment:

1. Confirm that the EC2 instances are running.
2. Check that Apache is serving the website on both instances.
3. Confirm that both instances are registered with the target group.
4. Check that the target group reports both instances as healthy.
5. Open the ALB DNS name in a browser.
6. Verify that the website is accessible through the load balancer.

## Security Considerations

- Do not upload Terraform state files to GitHub.
- Do not commit AWS credentials, private keys, or secrets.
- Restrict SSH access to trusted IP addresses.
- Prefer allowing EC2 HTTP traffic only from the ALB security group.
- Use HTTPS for production websites.
- Follow the principle of least privilege when granting AWS IAM permissions.

## Cleanup

AWS resources may incur charges while they exist.

After testing, review the resources and remove those created by this project when they are no longer needed.

If Terraform manages the resources and the state is available, run:

```bash
terraform destroy
```

Review the proposed deletions before confirming.

## Learning Outcomes

This project helps develop practical knowledge of:

- Terraform and Infrastructure as Code
- AWS networking and VPC configuration
- EC2 instance provisioning
- Apache web server deployment
- Amazon S3 object storage
- Application Load Balancer configuration
- Target groups and health checks
- AWS security groups
- Terraform plan, apply, and destroy workflows

## Author

Chandu Yadav

GitHub: https://github.com/chanduyadav334
