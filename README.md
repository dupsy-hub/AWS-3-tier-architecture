# AWS-3-tier-architecture
Overview

This repository contains a visual representation of a 3-Tier Architecture on AWS using Draw.io. The architecture follows the standard three-tier approach:

Presentation Layer: Handles user requests via Application Load Balancer (ALB) & EC2 instances.

Application Layer: Processes requests using backend servers.

Database Layer: Stores application data using Amazon RDS.


Components Used:
Frontend: 
  AWS CloudFront 
  Application Load Balancer (ALB)
  EC2 Instances
  Route 53

Backend:
  EC2 Instances
  Auto Scaling Group (ASG)
  IAM Roles
  
Database:
  Amazon RDS (MySQL)
  Networking
  Virtual Private Cloud (VPC)
  Subnets (Public & Private)
  Security Groups
  Route Tables

Security:
  Amazon Certificate Manager (ACM)
  Bastion Host
  
Monitoring:
  Amazon CloudWatch
  CloudWatch Alarms

Step-by-Step Implementation

1. Setting Up the VPC & Subnets

A VPC was created to provide an isolated and secure environment.

The VPC spans two Availability Zones (AZs) for fault tolerance.

Each AZ contains three subnets:

Public Subnet (Presentation Tier)

Private Subnet (Application Tier)

Private Subnet (Database Tier)

2. Database Layer (Amazon RDS)

Multi-AZ RDS setup was implemented for high availability.

The primary RDS instance is in the first AZ, while the standby RDS instance is in the second AZ.

Synchronous replication ensures data durability.

If failure occurs, automatic failover happens to the standby database.

3. Application Layer

Auto Scaling Group (ASG) is used to manage EC2 instances across two AZs.

The ASG scales the application tier based on demand.

An internal Application Load Balancer (ALB) is deployed to distribute traffic to the backend servers.

A bastion host is used to securely access the private instances.

4. Presentation Layer

An Internet-facing ALB manages external traffic.

Route 53 is configured for DNS resolution.

AWS Certificate Manager (ACM) issues an SSL certificate for secure HTTPS access.

Amazon CloudFront is integrated for content delivery optimization.

5. Monitoring & Security

Amazon CloudWatch collects logs and metrics for troubleshooting and performance analysis.

CloudWatch Alarms trigger scaling actions in the ASG.

Security measures include IAM roles, Security Groups, and SSL encryption.

Conclusion
This 3-Tier AWS Architecture ensures scalability, security, and high availability for applications. By leveraging AWS best practices, the architecture efficiently handles requests, processes data, and stores it securely while minimizing downtime.

