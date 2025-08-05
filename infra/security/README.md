# 🔐 Security Configuration - Lift and Shift vProfile Project

This document outlines the security groups and SSH key used to securely deploy the multi-tier vProfile application on AWS.

---

## ✅ Security Groups

### 1. `vprofile-ELB-SG` (Load Balancer)
- HTTP (80) and HTTPS (443) from anywhere
- Used by Application Load Balancer

### 2. `vprofile-app-sg` (Tomcat Instances)
- Port 8080 from Load Balancer SG
- Port 22 (SSH) from My IP

### 3. `vprofile-backend-sg` (DB, MQ, Cache)
- Ports 3306, 11211, 5672 from App SG
- Port 22 (SSH) from My IP
- All traffic from itself for inter-service communication

---

## 🔑 SSH Key
- **Key name**: `vprofile-prod-key.pem`
- Used to SSH into EC2 instances
- Do not share or commit this key anywhere
