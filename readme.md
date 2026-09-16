# Secure-AWS-Cloud-Infrastructure-Design


This project demonstrates how to migrate a legacy infrastructure to a secure, highly available, and scalable 3-tier cloud architecture on AWS that would aligned with NIST CSF 2.0 principles.

## --------- Goal------------

The goal to this project is to Transition the business of WinLocal Giveaways Ltd from an unsegmentaed Dublin data centre to a secure-by design AWS VPC to prevent any sorts of ransomeware lateral movement, remove service downtime, and ensure data integrity.

## ------What I Build--------

-Architected a multi-tier VPC across 2 Availability Zones (us-east-1a and us-east-1b).

-Isolated web servers in private subnets with no direct public IP addresses.

-Configured an Application Load Balancer (ALB) to manage inbound HTTP traffic.

-Deployed a hardened Bastion Host in a public subnet to act as a secure SSH jump box.

-Built a golden Amazon Machine Image (AMI) containing Amazon Linux 2023, Apache, and PHP.

-Set up an ASG (Auto Scaling Group) with capacity limits (Min: 1, Max: 2) triggered by CPU utilization.

-Provisioned an isolated Amazon RDS MySQL database in private DB subnets.

-Configured an Amazon S3 bucket with "Block All Public Access: ON" for secure asset storage.


### AWS Services Used

-Virtual Private Cloud (VPC)

-Elastic Compute Cloud (EC2) & AMIs 

-Auto Scaling Groups (ASG)

-Application Load Balancer (ALB)

-Relational Database Service (RDS MySQL)

-Simple Storage Service (S3)

-Identity and Access Management (IAM)

-Security Groups & Internet Gateway (IGW)


### Screenshots

-Bastion Host EC2 Instance Details

-Security Group Restricted SSH Access

-RDS Database Configuration & Endpoint Status

-Running Apache & PHP Web Server Execution

-Multi-Hop SSH Jump Sequence (Public to Private Subnet)

-Custom Amazon Machine Image (AMI) Golden Template

-Auto Scaling Group Capacity & Policy Setup

-Successful Database Connection Verification via Web Application

-S3 Storage Bucket Permissions & Object View

## -------How it works-------

-User request arrives at Application Load BalancerPublic traffic enters via the Internet Gateway (IGW) to the ALB on Port 80. The ALB inspects request health and routes traffic to web instances in private subnets.         Inbound Rule: HTTP Port 80 from 0.0.0.0/0

-Web server processes request in private isolationThe EC2 web server runs inside a private subnet without a public IP. It accepts traffic exclusively from the ALB Security Group.           Inbound Rule: HTTP Port 80 strictly from ALB-SG

-Web application communicates with private databaseThe PHP application queries the Amazon RDS MySQL instance residing inside isolated database subnets over Port 3306.  Inbound Rule: MySQL Port 3306 strictly from Web-Server-SG

-Administrator accesses internal instances via Bastion jumpAdmins connect to the public Bastion Host via SSH (Port 22) using key-pair authentication. From the Bastion, admins perform an internal SSH jump to reach internal web servers (e.g., 10.0.129.170).  Inbound Rule: SSH Port 22 strictly from Bastion-SG  

-Auto Scaling Group handles traffic spikes dynamically

When competition traffic pushes CPU utilization past 60%, ASG automatically launches an additional web instance from the pre-configured golden AMI. Once traffic normalizes, extra instances terminate to save operational costs.


## ------What I learned-------

-Designing multi-tier VPC network segmentation across Multi-AZ environments.

-Implementing "Defense-in-Depth" security principles using Security Groups and jump hosts.

-Creating custom AMIs and Auto Scaling policies for horizontal scalability.

-Isolating relational databases (RDS MySQL) in non-routable subnets.

-Mapping cloud infrastructure capabilities to the NIST Cybersecurity Framework (CSF 2.0).

## --Why this project matters--

This project demonstrates:

-Hands-on AWS cloud architecture design capabilities.

-Practical network security and attack surface reduction strategies.

-High availability, fault tolerance, and self-healing systems design.

-Business-focused cloud migration and cost optimization skills.