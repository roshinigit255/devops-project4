# AWS Three Tier Web Architecture 

## Description: 
Creating a three-tier web architecture in AWS. We will be manually creating the necessary network, security, app, and database components and configurations in order to run this architecture in an available and scalable manner.

## Architecture Overview
<img width="788" height="413" alt="image" src="https://github.com/user-attachments/assets/8333a257-2380-4b3c-8fb5-0f0ac4677bf1" />

In this architecture, a public-facing Application Load Balancer forwards client traffic to our web tier EC2 instances. The web tier is running Nginx webservers that are configured to serve a React.js website and redirects our API calls to the application tier’s internal facing load balancer. The internal facing load balancer then forwards that traffic to the application tier, which is written in Node.js. The application tier manipulates data in an Aurora MySQL multi-AZ database and returns it to our web tier. Load balancing, health checks and autoscaling groups are created at each layer to maintain the availability of this architecture.

## Algorithm
### AWS PROJECT
---

# Creating 3 Tier Architecture & Integrating Other AWS Resources

## Step 1: Download Code from GitHub in Your Local System

## Step 2: Create Two S3 Buckets
- Create one S3 bucket for storing web-server & app-server code.
- Upload the code to your S3 from your local system.
- Create another S3 bucket for VPC flow logs.
- <img width="959" height="249" alt="image" src="https://github.com/user-attachments/assets/4ee3ebb3-c430-43f8-9e0e-b49c562d5ec7" />


## Step 3: Create IAM Role with Policies
- S3 read only.
- SSM managed instance core.
- <img width="953" height="373" alt="image" src="https://github.com/user-attachments/assets/ff9b4f99-c18f-4b0c-8d6f-1218ff91a742" />


## Step 4: Create VPC, Subnets, IGW, NAT-GW, RT
- Enable auto-assign public IP for web-tier public subnets.
- Create flow logs for VPC & use the S3 bucket created above.
- <img width="954" height="447" alt="image" src="https://github.com/user-attachments/assets/a0946b84-9792-4a5d-a330-d8ce82c113a1" />


## Step 5: Create Security Groups
1. **External-Load-Balancer-SG** --> HTTP (80): 0.0.0.0/0.
2. **Web-Tier-SG** --> HTTP --> Ext-LB-SG.
3. **Internal-Load-Balancer-SG** --> HTTP --> Web-Tier-SG.
4. **App-Tier-SG** --> Port 4000 --> Internal-LB-SG.
5. **DB-Tier-SG** --> MySQL (3306) --> App-Tier-SG.
-   <img width="955" height="328" alt="image" src="https://github.com/user-attachments/assets/cf172d7e-95f4-443e-a4d1-ba0d51416232" />


## Step 6: Create DB Subnet Group & RDS
- Create DB subnet group.
- Create RDS - Multi-AZ.
- Place them in DB subnet group created above.

## Step 7: Create Test App Server, Install Packages, Test Connections
- [Test App-Server Commands](https://github.com/pandacloud1/AWS_Project1/blob/main/app-server-commands)
- Create AMI.
- Create launch template using AMI.
- Create target group.
- Create internal load balancer.
- Create autoscaling group.
- <img width="959" height="398" alt="image" src="https://github.com/user-attachments/assets/8115ccba-f7a7-4fae-9221-61a6236e0915" />

- Edit `nginx.conf` file in local system by adding Internal-LB-DNS & upload the file in S3.

## Step 8: Create Test Web Server, Install Packages (Nginx, Node.js (React)), Test Connections
- [Test Web-Server Commands](https://github.com/pandacloud1/AWS_Project1/blob/main/web-server-commands)
- Create AMI.
- Create launch template using AMI.
- Create target group.
- Create external load balancer.
- Create autoscaling group.
- <img width="957" height="365" alt="image" src="https://github.com/user-attachments/assets/f850a5e0-ab41-4073-96d4-dac14d384b99" />


## Step 9: Add External-ALB-DNS Record in Route 53

## Step 10: Create CloudWatch Alarms Along with SNS

## Step 11: Create CloudTrail
- <img width="942" height="347" alt="image" src="https://github.com/user-attachments/assets/550b8dda-9a15-4851-b829-948f11133541" />


## Step 12: Deleting the Entire Infrastructure
- Delete CloudFront.
- Delete CloudWatch alarms.
- Delete records from Route 53.
- Delete load balancers, target groups, ASG, launch templates.
- Delete security group.
- Delete NAT gateway (it will take 5 mins).
- Release elastic IP.
- Delete VPC.
- Delete RDS subnet group, RDS.

---


## Workshop Instructions:

See [AWS Three Tier Web Architecture](https://catalog.us-east-1.prod.workshops.aws/workshops/85cd2bb2-7f79-4e96-bdee-8078e469752a/en-US)
