# Secure & Monitored Web Infrastructure – foobar.com

This repository presents a basic **3-server web infrastructure** designed to host the website `www.foobar.com`.  
The architecture meets the following production-readiness requirements:

- ✅ HTTPS support (via SSL certificate)
- ✅ Monitoring enabled (via SumoLogic agent or another monitoring service)
- ✅ Firewalls for each component


---


## Infrastructure Design Overview

        [ User's Browser ]
                |
             HTTPS (port 443)
                |
           +------------------+
           |  HAProxy (LB)    | ← SSL Certificate + Monitoring
           +------------------+
                |         |
                v         v
        +----------------+  +----------------+
        | Firewall Srv 1 |  | Firewall Srv 2 |
        +----------------+  +----------------+
               |                    |
               v                    v
        +----------------+   +----------------+
        |   Server 1     |   |   Server 2     |
        | - Nginx        |   | - Nginx        |
        | - App Server   |   | - App Server   |
        | - Codebase     |   | - Codebase     |
        | - MySQL (P)    |   | - MySQL (R)    |
        | - Monitoring   |   | - Monitoring   |
        +----------------+   +----------------+
               ↘                ↙
           MySQL Replication (Primary ➝ Replica)


---


## Components & Their Purpose

### **1. SSL Certificate**

- Installed on HAProxy to serve the website via **HTTPS**.
- Ensures **secure and encrypted** communication between the client and the server.

### **2. Firewalls (3 total)**

- Each server and the load balancer are protected by a firewall.
- Filters inbound/outbound traffic, allowing only required ports.

### **3. Monitoring Clients**

- One agent per server (HAProxy + Server 1 + Server 2).
- Sends metrics and logs to a monitoring platform (**Sumologic**).
- Used to track:
  - Server uptime
  - Traffic
  - CPU, RAM
  - HTTP requests per second (QPS)
  - Errors

---

## Key Explanations

### 🔹 Why HTTPS?

- Prevents data interception and tampering.
- Provides trust and data integrity for users.

### 🔹 What are Firewalls for?

- Control incoming/outgoing traffic.
- Minimize attack surface by only exposing necessary services.

### 🔹 What is Monitoring Used For?

- Observability: detect outages, performance issues, anomalies.
- Debugging: review logs and metrics during incidents.
- Capacity planning: understand load patterns.

### 🔹 How Is Monitoring Data Collected?

- Monitoring agents read:
  - System metrics (CPU, RAM, disk)
  - Application logs (Nginx access/error logs)
- Data is sent to a centralized dashboard (Sumologic).

### 🔹 How to Monitor Web Server QPS?

- Use the monitoring agent to parse **Nginx access logs**.
- Count the number of requests per second.
- Visualize trends in the monitoring dashboard.


---


## ⚠️ Limitations & Risks of This Infrastructure

### 1. SSL Termination at the Load Balancer

- After the HAProxy decrypts the traffic, communication between HAProxy ➝ web servers is **unencrypted**.
- Possible man-in-the-middle risks within internal network.

### 2. Single Writable MySQL Server

- Only Server 1 can handle **write** operations.
- If it fails, write functionality is lost unless a manual failover is performed.

### 3. Identical Components on Both Servers

- Both servers contain **Web + App + DB**, which:
  - Is not optimal for **scaling** each layer independently.
  - Can lead to **resource contention** (CPU/RAM usage competing).
  - Increases maintenance complexity.


---


## Summary

This infrastructure is a good **starting point** for a small-to-medium production website:

- ✅ Secured with HTTPS and firewalls  
- ✅ Monitored via observability tools  
- ⚠️ Still contains SPOFs and architectural coupling  


---

> *This design is part of a systems architecture exercise to demonstrate understanding of modern web hosting, security, and monitoring concepts.*
