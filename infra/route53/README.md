# 🌐 Route 53 - Private DNS Configuration

This document describes how we configured internal DNS resolution between EC2 instances using Route 53 Private Hosted Zone.

---

## 🧩 Hosted Zone Info

- **Domain**: vprofile.in
- **Type**: Private
- **Region**: N. Virginia
- **VPC**: Default

---

## 🧾 DNS Records (A Records)

| Hostname            | Type | Private IP             | Description   |
|---------------------|------|------------------------|---------------|
| db01.vprofile.in    | A    | Private IP of DB       | MySQL DB      |
| mc01.vprofile.in    | A    | Private IP of Memcache | Memcached     |
| rmq01.vprofile.in   | A    | Private IP of RabbitMQ | RabbitMQ      |
| app01.vprofile.in   | A    | Private IP of App (optional) | Tomcat       |

---

## ✅ Verification

Run the following from `app01`:

```bash
ping -c 4 db01.vprofile.in
