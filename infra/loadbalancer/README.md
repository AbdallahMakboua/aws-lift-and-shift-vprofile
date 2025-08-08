# 🌐 Application Load Balancer Setup - vProfile Project

This document describes how we configured AWS ALB with optional HTTPS using ACM and domain mapping via GoDaddy.

---

## 🎯 Purpose

- Expose Tomcat app securely over the internet
- Enable HTTPS and custom domain access
- Validate backend service connectivity via UI

---

## 🧱 ALB & Target Group

- **Target Group**: `vprofile-las-tg` (HTTP, port 8080)
  - Health check port overridden to 8080
- **Load Balancer**: `vprofile-las-elb`
  - Listener: HTTP (80)
  - Listener: HTTPS (443) *(optional)* with ACM

---

## 🔐 SSL & Domain Setup

- **ACM Certificate**: Valid public SSL for `vprofileapp.example.com`
- **GoDaddy DNS**:
  - Type: CNAME
  - Name: `vprofileapp`
  - Value: `<ALB DNS Name>`

---

## ✅ Functional Testing

- Access: `http://vprofileapp.example.com`  
- Access: `https://vprofileapp.example.com`  
- Login with:
  - **User**: `admin_vp`
  - **Pass**: `admin`
- Validate:
  - DB (login success)
  - RabbitMQ (queue appears)
  - Memcache (user load = DB, reload = Cache)

