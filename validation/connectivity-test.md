# Connectivity Test Report

## Objective
Validate that public subnets have outbound internet access and private
subnets are isolated from direct internet connectivity.

---

## Test Environment

- Region: eu-west-2
- VPC: bootcamp-vpc
- Public Subnets:
  - public-subnet-a
  - public-subnet-b
- Private Subnets:
  - private-subnet-a
  - private-subnet-b

---

## Test 1: Public Subnet Internet Connectivity

### Setup
- Launched an EC2 instance in `public-subnet-a`
- Auto-assign public IPv4 enabled
- Security group allowed outbound traffic
- Connected to the instance via SSH

### Test Performed
Executed outbound connectivity checks:
- `ping 8.8.8.8`
- `curl https://example.com`

### Expected Result
The instance should be able to reach the internet via the Internet Gateway.

### Actual Result
The instance successfully reached external internet endpoints.

### Outcome
Public subnet has outbound internet connectivity.

---

## Test 2: Private Subnet Internet Isolation

### Setup
- Launched an EC2 instance in `private-subnet-a`
- No public IP assigned
- Subnet associated with a route table that has no Internet Gateway route

### Test Performed
Attempted outbound internet access from the instance.

### Expected Result
The instance should not be able to access the internet.

### Actual Result
The instance was unable to reach external internet endpoints.

### Outcome
Private subnet has no direct internet access (expected behavior).

---

## Conclusion

The connectivity tests confirm that:
- Public subnets are correctly configured with internet access via an Internet Gateway.
- Private subnets are isolated and cannot access the internet directly.

This validates correct subnet segmentation and routing configuration within the VPC.
