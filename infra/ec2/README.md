# 🚀 EC2 Provisioning - vProfile Lift & Shift

This document outlines the EC2 instances used in this project and how they were provisioned using user data scripts.

---

## 🔧 Instances Launched

| Instance Name     | Role         | AMI                   | Security Group         | Script         |
|------------------|--------------|------------------------|------------------------|----------------|
| vprofile-db01     | MySQL        | Amazon Linux 2023      | vprofile-backend-sg    | mysql.sh       |
| vprofile-mc01     | Memcached    | Amazon Linux 2023      | vprofile-backend-sg    | memcache.sh    |
| vprofile-rmq01    | RabbitMQ     | Amazon Linux 2023      | vprofile-backend-sg    | rabbitmq.sh    |
| vprofile-app01    | Tomcat       | Ubuntu 24.04 LTS       | vprofile-app-sg        | tomcat_ubuntu.sh |

---

## 🛡 Best Practices Followed

- Used official AMIs with minimum OS customization
- Applied the principle of least privilege in Security Groups
- Tagged all instances and volumes (`Name`, `Project`)
- Validated services post-deployment
- Used `user-data` scripts for full automation (IaC style)

---

## 🔗 Scripts Used

The scripts can be found in:
