# Highly Available 3-Tier Architecture on AWS

This repository documents a **hands-on 3-tier architecture** built on AWS via the Management Console.  
It’s a reference for understanding how networking, compute, and databases work together in a production-ready environment.

## Architecture Overview

![Architecture](architecture/3-tier.png)


The solution includes the following components:

- Web Tier (Apache)
- Application Tier (App server)
- Database Tier (Amazon RDS MariaDB)
- Security and networking (VPC, subnets, route tables, security groups)
- Auto Scaling Groups and Launch Templates

## Quick Setup Overview

1. **VPC & Subnets:** 1 public, 3 private across 2 AZs  
2. **Internet & NAT Gateways:** IGW attached to VPC; NAT Gateway in public subnet  
3. **Route Tables:** Public routes → IGW, Private routes → NAT Gateway  
4. **Security Groups:** Web, App, Database  
5. **Servers:** Launch EC2 instances via console, configure user data for web & app servers  
6. **Database:** RDS MariaDB in private subnets  