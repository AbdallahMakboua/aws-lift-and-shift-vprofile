# ⚙️ Auto Scaling Group - vProfile App

This document details the setup of an Auto Scaling Group (ASG) for the `app01` instance of the vProfile project, enabling horizontal scaling based on CPU usage.

---

## 🧱 Components

- **AMI**: `vprofile-las-app-ami` (created from `app01`)
- **Launch Template**: `vprofile-las-app-LT`
- **Auto Scaling Group**: `vprofile-las-app-asg`
- **Target Group**: `vprofile-las-tg` (used by ALB)
- **Load Balancer**: `vprofile-las-elb`

---

## 🚀 Configuration Summary

| Parameter         | Value                      |
|-------------------|----------------------------|
| Instance Type     | t3.micro                   |
| Desired Capacity  | 1                          |
| Min Size          | 1                          |
| Max Size          | 4                          |
| Scaling Policy    | CPU > 50% = scale out      |
| Stickiness        | Enabled (cookie-based)     |
| Health Check Type | ELB-based (port 8080)      |

---

## 🔁 Lifecycle

1. **AMI** created from `app01`
2. **Launch Template** created using AMI
3. **ASG** created referencing launch template
4. **New instances** registered to Target Group
5. **app01** terminated manually

---

## 🧪 Testing

- ✅ Login success → DB working
- ✅ View user → Memcache working
- ✅ Queue generated → RabbitMQ working
- ✅ Sticky sessions → Session persists across reloads

---

## 🔒 Notes

- IAM Role (`S3Admin`) not required here, but may be used in Jenkins pipeline later.
- For production: Set appropriate cooldown and detailed metric alarms
