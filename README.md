# AWS-3-tier-architecture
Overview
This repository contains a visual representation of a 3-Tier Architecture on AWS using Draw.io. The architecture follows the standard:
- Presentation Layer: Handles user requests via Application Load Balancer & EC2 instances.
- Application Layer: Processes requests using backend servers.
- Database Layer: Stores application data using Amazon RDS.


Components Used
- Frontend: AWS CloudFront, Application Load Balancer, EC2 Instances, Route53. 
- Backend: EC2, Auto Scaling Group, IAM Role.
- Database: Amazon RDS (MySQL).
- Networking: VPC,Subnets,  Security Groups, Route Tables.
- Security: Amazon Certificate Manager (ACM), Bastion Host.
- Monitoring: CloudWatch, CloudWatch Alarm.

Step-by-Step Implementation 
Setting Up the VPC & Subnets
I created a VPC to provide an isolated network and enhanced security for my resources.
For fault tolerance and availability, the VPC was divided into 2 Availability Zones (AZ). Each AZ contained 3 Subnets; 
1 Public Subnet for  the Presentation tier
1 Private Subnet for the Application Tier
1 Private Subnet for the Database Tier

For data durability and resilience, I implemented Multi-AZ Relational Database (RDS) setup, with the primary RDS in the private subnet for the database tier of the 1st AZ, and the standby RDS  in the private subnet for the  database tier of the 2nd AZ. This ensured business continuity in case of failures or disruptions in the primary database.

An Auto  Scaling Group (ASG) was used to automatically scale the application tier to meet fluctuating demand with the ASG managing EC2 instances across the 2 AZs.
To manage the presentation tier, I also implemented an ASG to ensure high availability and performance

A bastion host was deployed to securely access the instances. It served as a control entry point to the private network so that the application tier is not accessed directly.

To efficiently distribute traffic within the application tier, an internal Application Load Balancer (ALB) was implemented. The ALB will direct traffic across the EC2 instances in the private subnet.

To manage external traffic, I deployed an internet facing ALB that distributes traffic across the presentation tier instances. This 2 tier ALB approach enhances scalability and performance.

To efficiently manage DNS resolution and ensure secure communication, I leverage Amazon Route53. By creating DNS records within Route53, my domain will be mapped to the appropriate resources.

For secure HTTPS connections, SSL certificate from AWS Certificate Manager (ACM) was also procured. This certificate was integrated with CloudFront, a content delivery network (CDN) to encrypt data in transit and optimize content delivery to end users. With all these components in place, users can securly access the application via HTTPS.

There is synchronous replication of data between the primary database and the standby database for high availability. So in the event of failure, RDS automatically transitions to the standby instance, minimizing downtime and data loss.

To enhance monitoring and optimize resource utilization, I integrated CloudWatch into the architecture. Application logs will be centrally managed within CloudWatch logs providing easy access for troubleshooting and performance analysis.

CloudWatch Alarm was also configured to trigger scaling actions within the ASG ensuring optimal resource allocation based on the demand. By scaling out during peak usage and scaling in during low traffic periods, cost efficiency is manitained while delivering consistent performance.
