# 🚀 Artifact Build & Deployment (vProfile)

This document describes how the vProfile WAR file is built locally and deployed to the Tomcat EC2 instance via S3.

---

## 🧱 Artifact Build

- Tool: Apache Maven 3.9.9
- JDK: Java 17
- Output: `target/vprofile-v2.war`

## 🧩 S3 Bucket

- Bucket: `vprofile-las-artifacts-[unique]`
- Region: N. Virginia
- Used to store WAR artifact before deployment

## 🛡 IAM Setup

| Resource     | Type       | Permissions         |
|--------------|------------|---------------------|
| IAM User     | `vprofile-s3-admin` | AmazonS3FullAccess |
| IAM Role     | `S3Admin`           | AmazonS3FullAccess (attached to `app01`) |

---

## 🛠 Deployment on EC2 (Ubuntu)

```bash
sudo snap install aws-cli --classic
aws s3 cp s3://vprofile-las-artifacts-[unique]/vprofile-v2.war /tmp/
sudo systemctl stop tomcat10
sudo rm -rf /var/lib/tomcat10/webapps/ROOT
sudo cp /tmp/vprofile-v2.war /var/lib/tomcat10/webapps/ROOT.war
sudo systemctl start tomcat10
