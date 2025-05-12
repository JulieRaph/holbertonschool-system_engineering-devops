# 🌐 Web Infrastructure Design for www.foobar.com

## 📊 Architecture Diagram

                             +---------------------+
                             |     Web Browser     |
                             |   www.foobar.com    |
                             +----------+----------+
                                        |
                                        | HTTP Request (port 80)
                                        v
                            +-----------+------------+
                            |     Load Balancer      |
                            |        (HAProxy)       |
                            | Algorithm: Round Robin |
                            +-----------+------------+
                                        |
                    +-------------------+-------------------+
                    |                                       |
                    v                                       v
       +------------------------+              +------------------------+
       |        Server 1        |              |        Server 2        |
       |------------------------|              |------------------------|
       |  - Nginx (Web Server)  |              |  - Nginx (Web Server)  |
       |  - Application Server  |              |  - Application Server  |
       |  - Application Files   |              |  - Application Files   |
       |  - MySQL (Primary DB)  |              |  - MySQL (Replica DB)  |
       +-----------+------------+              +-----------+------------+
                   |                                         ^
                   |  Write operations                      |
                   |  (INSERT, UPDATE, DELETE)              |
                   |----------------------------------------+
                   |      One-way Replication (Read-only)
                   v
        Application reads/writes based on request type


---

## 🔍 Component Descriptions

### 🔹 Load Balancer (HAProxy)

- **Purpose**: Distributes incoming traffic between the two servers to balance the load.
- **Load distribution algorithm**: `Round Robin`
  - Each incoming request is forwarded to a different backend server in a circular order.
- **Configuration**: `Active-Active`
  - Both servers are active simultaneously and handle user requests concurrently.
  - Difference:
    - **Active-Active**: Both servers are online and load-balanced.
    - **Active-Passive**: One server is active, the other is on standby for failover.

---

### 🔹 Web & Application Servers (x2)

Each of the two servers includes:
- `Nginx`: Serves static files and handles HTTP requests.
- `Application Server` (e.g., PHP, Node.js): Processes business logic.
- `Application Code Base`: Files containing the website's source code.
- `MySQL Database`:
  - **Server 1** hosts the **Primary** database.
  - **Server 2** hosts the **Replica** database.

---

### 🔹 Database Cluster (Primary-Replica)

- **Primary (Master)**:
  - Handles all **write operations**: inserts, updates, deletions.
- **Replica (Slave)**:
  - Receives a **read-only copy** of the Primary's data.
  - Used for **read queries** to reduce load on the Primary.
- **Replication**: One-way, from Primary to Replica.
- This setup improves performance and data availability.

---

## ⚠️ Infrastructure Issues & Limitations

### ❌ Single Points of Failure (SPOFs)

- **HAProxy**:
  - If the load balancer fails, the entire website becomes inaccessible.
- **Primary Database**:
  - If it goes down, all write operations are blocked.

### 🔐 Security Concerns

- **No firewall**:
  - Open access to services can be exploited.
- **No HTTPS**:
  - HTTP traffic is unencrypted and can be intercepted by attackers.

### 📉 No Monitoring

- There is no system in place to monitor server health, performance, or downtime.
- Failures may go unnoticed until reported by users.

---

## ✅ Summary

This web infrastructure improves availability and scalability through load balancing and database replication. However, it still has critical points of failure and lacks essential security and monitoring features, which would need to be addressed in a production-grade setup.
