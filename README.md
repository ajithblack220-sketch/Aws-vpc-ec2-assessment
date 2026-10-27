# Aws-vpc-ec2-assessment
Aws vpc networking and linux ec2 deployment project 

AWS VPC and Linux EC2 Deployment
Project Overview

This project demonstrates the setup of an Amazon Virtual Private Cloud (VPC), including public and private subnets, an Internet Gateway, route tables, security groups, and a Linux EC2 instance.

The Linux EC2 instance is deployed in the public subnet and accessed using AWS EC2 Instance Connect.

The project demonstrates fundamental AWS networking, compute, connectivity, and security concepts.

Objectives

Create an AWS VPC with a custom IPv4 CIDR block.
Create a public subnet and a private subnet, each containing 256 IPv4 addresses.
Create and attach an Internet Gateway to the VPC.
Configure route tables for public and private subnets.
Launch a Linux EC2 instance in the public subnet.
Configure security group rules for SSH connectivity.
Connect to the Linux instance using EC2 Instance Connect.
Document the implementation with screenshots.
Technologies Used
Amazon VPC
Amazon EC2
Amazon Linux 2023
Internet Gateway
Route Tables
Security Groups
EC2 Instance Connect
GitHub
Architecture

                    AWS Cloud
                        |
                 +-------------+
                 |     VPC     |
                 | 10.0.0.0/23 |
                 +-------------+
                        |
                 +-------------+
                 | Internet    |
                 | Gateway     |
                 +-------------+
                        |
                Public Route Table
                0.0.0.0/0 -> IGW
                        |
              +-------------------+
              |   Public Subnet   |
              |   10.0.0.0/24     |
              |                   |
              |  Linux EC2        |
              |  Instance         |
              +-------------------+

              +-------------------+
              |   Private Subnet  |
              |   10.0.1.0/24     |
              |                   |
              |  Internal         |
              |  Resources        |
              +-------------------+
                        |
                Private Route Table
                Local route only

Network Configuration
Resource	Configuration
VPC name	assessment-vpc
VPC CIDR	10.0.0.0/23
Public subnet	assessment-public-subnet
Public subnet CIDR	10.0.0.0/24
Private subnet	assessment-private-subnet
Private subnet CIDR	10.0.1.0/24
Internet Gateway	assessment-igw
Public route table	assessment-public-rt
Private route table	assessment-private-rt
EC2 instance name	assessment-linux-instance
Operating system	Amazon Linux 2023
SSH port	TCP 22
Access method	EC2 Instance Connect

Each /24 subnet contains 256 IPv4 addresses. AWS reserves five addresses per IPv4 subnet, leaving 251 usable addresses for AWS resources.

Implementation Steps
1. Create the VPC

Created a custom VPC with the IPv4 CIDR block 10.0.0.0/23.

2. Create the public subnet

Created assessment-public-subnet with CIDR 10.0.0.0/24 and configured public IPv4 address assignment.

3. Create the private subnet

Created assessment-private-subnet with CIDR 10.0.1.0/24 for resources that do not require direct internet access.

4. Configure the Internet Gateway

Created assessment-igw and attached it to the VPC.

5. Configure route tables

Created separate route tables for the public and private subnets.

Public route table

Destination	Target
10.0.0.0/23	Local
0.0.0.0/0	Internet Gateway

Private route table

Destination	Target
10.0.0.0/23	Local

The private route table does not contain a direct Internet Gateway route.

6. Launch the Linux EC2 instance

Launched an Amazon Linux 2023 EC2 instance in the public subnet with a public IPv4 address.

7. Configure security groups

Configured inbound security group rules for SSH connectivity. Added the regional EC2 Instance Connect managed prefix list to permit browser-based EC2 Instance Connect access.

SSH access from an administrator's computer can be restricted to the administrator's public IP address.

8. Connect to the Linux instance

Connected successfully to the running Linux EC2 instance using AWS EC2 Instance Connect.

Validation and Results

The following checks were performed during implementation:

VPC created with the specified IPv4 CIDR.
Public and private subnets created successfully.
Internet Gateway attached to the VPC.
Public route table configured with a default route to the Internet Gateway.
Private subnet associated with its private route table.
Linux EC2 instance launched in the public subnet.
EC2 instance status checks passed.
Security group configured for EC2 Instance Connect.
Browser-based connection to the Linux instance succeeded.
Screenshots

The screenshots/ directory contains evidence of the AWS implementation.

Screenshot	Description
01-vpc-created.png	VPC configuration
02-public-subnet.png	Public subnet configuration
03-private-subnet.png	Private subnet configuration
04-internet-gateway.png	Internet Gateway attachment
05-public-route-table.png	Public route table configuration
06-private-route-table.png	Private route table configuration
07-ec2-running.png	Running Linux EC2 instance
08-linux-connection.png	Successful Linux connection
09-security-group.png	Security group inbound rules
10-public-route-table.png	Public internet route verification

Ensure these filenames match the screenshots actually uploaded to the repository.

Security Considerations
SSH access should be restricted to trusted sources.
Browser-based EC2 Instance Connect access should use the appropriate regional managed prefix list.
AWS credentials and private SSH keys must never be committed to GitHub.
Public HTTP and HTTPS rules should only be enabled when required by the application.
Private subnets should not have direct internet routes unless the architecture specifically requires them.
Learning Outcomes

Through this project, I gained practical experience with:

AWS VPC and IPv4 CIDR planning.
Public and private subnet configuration.
Internet Gateway and route table configuration.
EC2 instance deployment.
Security group configuration.
Browser-based Linux connectivity troubleshooting.
Technical documentation and version control using GitHub.

Conclusion
This project demonstrates the deployment of a Linux EC2 instance within a custom AWS VPC, supported by public and private subnet configurations, an Internet Gateway, route tables, and security group rules.

The instance was successfully accessed through AWS EC2 Instance Connect, and screenshots were captured to document the implementation.

