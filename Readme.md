# AWS Application Load Balancer Project

This project demonstrates how to deploy a secure and scalable web application on AWS using an Application Load Balancer (ALB) with path-based routing, a custom domain, and HTTPS integration.

---

## 1. Overview

The goal of this project is to simulate a production-ready cloud environment with proper network isolation, routing, and security configurations.

Key steps:
- Created a **VPC** with **three public** and **three private subnets** across multiple **Availability Zones**.  
- Launched **EC2 instances** inside private subnets to host the web application.  
- Configured an **Application Load Balancer (ALB)** in public subnets to handle external requests.  
- Implemented **path-based routing** for different sections:  
  - `/` → Home page  
  - `/orders` → Orders page  
  - `/accounts` → Account page  
- Mapped the **ALB DNS** to a custom domain **(chintaniskoda.xyz)** using **Route 53**.  
- Integrated **HTTPS** using **AWS Certificate Manager (ACM)** and redirected all HTTP traffic to HTTPS.  
- Ensured **security isolation** by keeping backend EC2 servers in private subnets while exposing only the ALB to the public.

---

## 2. Architecture Flow

    ┌──────────────────────────────┐
    │        Client (Browser)      │
    └──────────────┬───────────────┘
                   │
                   ▼
         [ HTTPS Request to ALB ]
                   │
                   ▼
    ┌──────────────────────────────┐
    │  Application Load Balancer   │
    │  - Terminates client request │
    │  - Acts as Reverse Proxy     │
    │  - Path-based Routing        │
    └──────────────┬───────────────┘
                   │
                   ▼
    ┌──────────────────────────────┐
    │     Target Group (Private)   │
    │     - EC2 Instances          │
    │     - Application hosted     │
    └──────────────┬───────────────┘
                   │
                   ▼
        [ Response sent back to ALB ]
                   │
                   ▼
        [ ALB sends response to Client ]

---

## 3. AWS Services Used

- **VPC** – Custom virtual private cloud for network isolation  
- **Subnets** – 3 public and 3 private subnets across different AZs  
- **EC2** – Application servers hosted privately  
- **Application Load Balancer (ALB)** – For load distribution and path-based routing  
- **Target Groups** – Registered private EC2 instances for routing and health checks  
- **Route 53** – Domain management and DNS routing  
- **AWS Certificate Manager (ACM)** – SSL/TLS certificate for HTTPS  
- **Security Groups** – Controlled inbound/outbound network access  

---

## 4. Security Highlights

- Application servers are hosted **inside private subnets**, preventing direct internet access.  
- The **Application Load Balancer acts as a Reverse Proxy** — it **terminates client connections**, processes requests, and forwards them securely to private EC2 instances.  
- The **ALB handles all responses** back to clients, ensuring a **controlled and secure communication flow**.  
- Configured **end-to-end HTTPS encryption** to secure data in transit.  
- Restricted inbound rules so that **only the ALB** can communicate with private EC2 instances.

---

## 5. Result

A fully functional, secure, and domain-mapped web application running behind an AWS Application Load Balancer, featuring:
- **Reverse proxy behavior**
- **Private backend isolation**
- **Dynamic path-based routing**
- **End-to-end HTTPS security**
- **Scalable and production-ready architecture**
