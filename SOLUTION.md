# Production-Ready VPC Deployment

## Overview

This project demonstrates the design and implementation of a
production-style VPC in AWS with proper public and private subnet
segmentation across multiple Availability Zones.

The objective was to ensure:
- Public subnets have controlled internet access
- Private subnets remain isolated
- High availability across two Availability Zones
- Clear routing separation

---

# 1. Network Design Explanation

The VPC was designed using a multi-AZ architecture to provide
fault tolerance and high availability.

Each Availability Zone contains:
- 1 Public Subnet (internet-facing resources)
- 1 Private Subnet (internal resources)

Internet access is controlled via:
- An Internet Gateway attached to the VPC
- A dedicated public route table with a default route (0.0.0.0/0)
- No default route in private route tables

This ensures public resources can access the internet while private
resources remain isolated.

---

# 2. CIDR Block Planning

## VPC CIDR
10.0.0.0/16

The /16 range was chosen to allow flexible subnet expansion
while maintaining clear segmentation.

## Subnet Allocation

Availability Zone: eu-west-2a
- Public Subnet: 10.0.1.0/24
- Private Subnet: 10.0.11.0/24

Availability Zone: eu-west-2b
- Public Subnet: 10.0.2.0/24
- Private Subnet: 10.0.12.0/24

Each subnet uses a /24 range (256 IPs), which is suitable for
small-to-medium workloads and allows clean separation between
public and private resources.

---

# 3. Step-by-Step Implementation Process

1. Created VPC with CIDR block 10.0.0.0/16
2. Created and attached an Internet Gateway
3. Designed subnet layout across two Availability Zones
4. Created 4 subnets (2 public, 2 private)
5. Enabled auto-assign public IP on public subnets only
6. Created separate route tables:
   - public-rt
   - private-rt
7. Added default route (0.0.0.0/0 → IGW) to public route table
8. Associated route tables with correct subnets
9. Launched EC2 instances to validate connectivity
10. Confirmed:
    - Public subnets had internet access
    - Private subnets had no internet access

---

# 4. Architecture Diagram

The architecture consists of:

- 1 VPC (10.0.0.0/16)
- 2 Availability Zones
- 4 Subnets
- 1 Internet Gateway
- 2 Route Tables

Diagram includes:
- VPC boundary
- Public and private subnet segmentation
- Route table associations
- Internet Gateway connection

