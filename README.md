# AWS-VPC-Architecture

## Project Summary 
This example demonstrates how to create a VPC that you can use for servers in a
production environment.
To improve resiliency, you deploy the servers in two Availability Zones, by using
an Auto Scaling group and an Application Load Balancer. For additional security,
you deploy the servers in private subnets. The servers receive requests through
the load balancer. The servers can connect to the internet by using a NAT
gateway. To improve resiliency, you deploy the NAT gateway in both Availability
Zones.

## Overview -
The VPC has public subnets and private subnets in two Availability Zones
Each public subnet contains a NAT gateway and a load balancer node.
The servers run in the private subnets, are launched and terminated by using an
Auto Scaling group, and receive traffic from the load balancer.
The servers can connect to the internet by using the NAT gateway.

## Prerequisites:
Before you get started, make sure you have the following prerequisites set:

- An Aws account

## Project Scope

- Design and configure a VPC: Create a VPC with custom IP ranges. Set up public and private subnets. Configure route tables and associate subnets.

- Implement network security: Set up network access control lists (ACLs) to control inbound and outbound traffic. Configure security groups for EC2 instances to allow specific ports and protocols.

- Provision EC2 instances: Launch EC2 instances in both the public and private subnets. Configure security groups for the instances to allow necessary traffic. Create and assign IAM roles to the instances with appropriate permissions.

- Networking and routing: Set up an internet gateway to allow internet access for instances in the public subnet. Configure NAT gateway or NAT instance to enable outbound internet access for instances in the private subnet. Create appropriate route tables and associate them with the subnets.

- SSH key pair and access control: Generate an SSH key pair and securely store the private key. Configure the instances to allow SSH access only with the generated key pair. Implement IAM policies and roles to control access and permissions to AWS resources.

- Test and validate the setup: SSH into the EC2 instances using the private key and verify connectivity. Test network connectivity between instances in different subnets. Validate security group rules and network ACL settings.

- By implementing this project, you'll gain hands-on experience in setting up a secure VPC with EC2 instances, implementing networking and routing, configuring security groups and IAM roles, and ensuring proper access control. This project will provide a practical understanding of how these AWS services work together to create a secure and scalable infrastructure for your applications.

## Implentation:
### 1. Create a VPC:

- Go to the AWS Management Console, navigate to the VPC dashboard, and click "Your VPCs."
- Click "Create VPC."
- Enter a name (e.g., MyMultiTierVPC), and define the IPv4 CIDR block (e.g., 10.0.0.0/16).
- Choose two Availability Zones.

### 2. Create Public and Private Subnets:

- For each Availability Zone, create a public and a private subnet.
For example, in the first Availability Zone:
Public subnet: CIDR block - 10.0.0.0/24
Private subnet: CIDR block - 10.0.1.0/24
- Repeat this for the second Availability Zone.

### 3. Create an Internet Gateway:

- In the VPC dashboard, click "Internet Gateways."
- Click "Create Internet Gateway" and name it (e.g., MyIGW).
- Attach it to your VPC.

### 4. Create Route Tables:

- Create two route tables: one for public subnets and one for private subnets.
- Name them, for instance, "PublicRouteTable" and "PrivateRouteTable."
- Edit the public route table and add a route to the Internet Gateway (0.0.0.0/0 via the Internet Gateway).
- Attach the public route table to the public subnets and the private route table to the private subnets.

### 5. Create a Network Address Translation (NAT) Gateway:

- In the VPC dashboard, click "NAT Gateways."
- Click "Create NAT Gateway" and choose the public subnet for the first Availability Zone.
- Allocate an Elastic IP address (or create one if needed).
- Repeat this for the second Availability Zone.

### 6. Create Security Groups and Network ACLs:

- Define security groups for your resources to control inbound and outbound traffic. For example, create a security group for your web servers, one for your application servers, and one for your database servers.
- Configure Network ACLs for additional network-level security if required.

### 7. Set Up Load Balancers:

- Create an Application Load Balancer (ALB) for your public subnets:
Name: MyALB
Listener: Port 80 (HTTP)
Target Group: Create a new target group
- Configure rules and actions to distribute incoming traffic to your web servers in the private subnets.

### 8. Launch and Configure Auto Scaling Group:

- Create an Auto Scaling group for your application servers:
- Choose your desired AMI, instance type, and other launch configuration settings.
- Configure scaling policies based on metrics like CPU utilization to automatically add or remove instances from the Auto Scaling group.

### 9. Security and IAM Policies:

- Define security policies and IAM roles for your instances to access other AWS services. For example, if you're using Amazon RDS, configure your security group and IAM role to allow your application servers to access the database.

### 10. Test and Monitor:

Launch instances in your private subnets and test connectivity through the load balancer.
Monitor your architecture using AWS CloudWatch to track performance, scaling, and other metrics.
Implement regular backups and disaster recovery procedures for critical data and resources.
  
