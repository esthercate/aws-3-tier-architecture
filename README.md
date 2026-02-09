# Highly Available 3-Tier Architecture on AWS

This repository documents a **hands-on 3-tier architecture** built on AWS via the Management Console.  
It’s a reference for understanding how networking, compute, and databases work together in a production-ready environment.

## Architecture Overview

![Architecture](architecture/3-tier.png)



The solution includes the following components:

- **Web Tier:** EC2 instances in a public subnet, behind an ALB  
- **Application Tier:** EC2 instances in a private subnet  
- **Database Tier:** Amazon RDS (MariaDB) in private subnets for security and HA  
- **Supporting Components:**  
  - VPC with public & private subnets across 2 Availability Zones  
  - NAT Gateway for private subnet internet access  
  - Security Groups to control traffic flow

  ## The Three Tiers
**1. Web (User/Presentation) Tier**

- Purpose: Handles incoming requests from users, serving web pages or APIs.

- Components: EC2 instances running a web server (Apache & PHP), optionally behind an Application Load Balancer (ALB).

- Placement: Public subnet, accessible from the internet.

- Security:

 - HTTP/HTTPS traffic allowed from anywhere

 - SSH access only via Bastion Host

Key Idea: The “front door” of your application — directly interacts with users and forwards requests to the application tier.

**2. Application (Logic) Tier**

- Purpose: Processes business logic, handles requests from the web tier, and communicates with the database.

- Components: EC2 instances running the application backend.

- Placement: Private subnet (no direct internet access).

- Security:

 - Receives requests only from the Web Tier

 - Connects to the Database Tier


Key Idea: The “brain” of your system, separating business logic from the user-facing layer for security, scalability, and manageability.

**3. Database (Data) Tier**

- Purpose: Stores and manages persistent application data.

- Components: Amazon RDS (MariaDB) instances deployed in private subnets.

- Placement: Private subnets, optionally across multiple Availability Zones for high availability.

- Security:

 - Accessible only from the Application Tier

 - No direct internet access

Key Idea: The “data backbone” of your application — keeps information secure, consistent, and highly available.

## Quick Setup Overview

1. **VPC & Subnets:** 1 public, 3 private across 2 AZs  
2. **Internet & NAT Gateways:** IGW attached to VPC; NAT Gateway in public subnet  
3. **Route Tables:** Public routes → IGW, Private routes → NAT Gateway  
4. **Security Groups:** Web, App, Database  
5. **Servers:** Launch EC2 instances via console, configure user data for web & app servers  
6. **Database:** RDS MariaDB in private subnets  

## References

For a detailed step-by-step walkthrough with screenshots, see my [blog post](https://medium.com/@vuthi.esther/a-simple-guide-to-building-a-highly-available-3-tier-architecture-on-aws-72b9d1bf2988)

## License

This project is licensed under the MIT License.