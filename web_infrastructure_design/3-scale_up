# Web Infrastructure with HAProxy Cluster and Separated Roles

## Objective

This infrastructure is designed to host the website **www.foobar.com**, with a focus on **availability**, **modularity**, and **clean separation of roles**. The goal is to improve scalability, reduce points of failure, and follow good architecture practices by assigning each component its own dedicated server.

## Infrastructure Overview

The infrastructure includes the following components:

- Two load balancers (HAProxy), configured in a high-availability cluster.
- One dedicated web server (Nginx).
- One dedicated application server (Node.js, PHP, etc.).
- One dedicated database server (MySQL).
- One additional server added to allow role separation or redundancy.

All traffic to www.foobar.com is served over HTTPS via an SSL certificate configured on both load balancers.

## Architecture (Text Diagram)

    User Request (HTTPS)
            |
    +----------------------+
    | Load Balancer #1     |
    | (HAProxy + SSL cert) |
    +----------------------+
            |
   (High availability cluster)
            |
   +----------------------+
   | Load Balancer #2     |
   | (HAProxy + SSL cert) |
   +----------------------+
            |
     Load balancing logic
            |
      +-------------+
      |             |
+-------------+  +-------------+
| Web Server  |  | Web Server  |
| (Nginx)     |  | (Nginx)     |
+-------------+  +-------------+
      |             |
      +-------------+
            |
     Application Server
       (Business Logic)
            |
     Database Server
         (MySQL)


## Explanation of Each Element

### Load Balancer Cluster (HAProxy)

Two HAProxy servers are configured in an active-passive high availability cluster. One is active, the other is on standby. If the active load balancer fails, the second one takes over automatically. This setup prevents a single point of failure at the network entry point.

### Web Server (Nginx)

This server handles all incoming HTTP/HTTPS requests. It serves static content and forwards dynamic requests to the application server. By isolating this component, it becomes easier to optimize and scale independently.

### Application Server

This server runs the business logic of the application. It processes requests received from the web server and communicates with the database when needed. Separation improves performance and maintainability.

### Database Server (MySQL)

This server stores and manages persistent data. It handles all read/write database operations. In this setup, a single primary server is used.

## Why This Architecture?

- **Separation of concerns**: Each server performs a single role, which simplifies maintenance and scalability.
- **High availability at the entry point**: A cluster of two load balancers ensures uninterrupted access to the site.
- **Independent scaling**: You can scale the web, application, and database layers separately depending on your needs.
