# Single-Server Web Architecture for www.foobar.com

## 1. Architecture Overview

- **User (browser)**: A person uses a web browser to access the website.
- **Domain Name (www.foobar.com)**: A human-readable address pointing to the IP **8.8.8.8**, thanks to a DNS A record.
- **Single Server (IP: 8.8.8.8)**: One server hosts **all components** of the application.

On this server, we find:
- **Web Server (Nginx)**: Handles incoming HTTP requests and serves static files or forwards dynamic requests to the application server.
- **Application Server**: Executes the application code (PHP, Python, Node.js, etc.) and handles business logic.
- **Application Files (Code Base)**: Includes static files (HTML, CSS, JS) and backend code.
- **Database (MySQL)**: Stores all persistent data (users, content, etc.).

This is a typical **LEMP** stack: Linux, Nginx, MySQL, and a backend language (e.g. PHP).

---

## 2. User Request Flow

1. **User enters "www.foobar.com" in their browser**.
2. **The browser queries DNS**, which resolves the domain name to the IP address **8.8.8.8**.
3. **An HTTP request is sent to 8.8.8.8** on port 80.
4. **Nginx receives the request**:
   - If it's a static file (e.g. image, CSS), Nginx serves it directly.
   - If it's a dynamic request (e.g. API, PHP page), Nginx forwards it to the application server.
5. **The application server processes the logic** and queries the **MySQL database** if needed.
6. **A response is generated** (HTML or JSON).
7. **The response goes back through Nginx** and is sent to the browser.
8. **The browser renders the page** for the user.

---

## 3. Component Roles

- **Server**: A machine that hosts the web server, application server, and database.
- **Domain Name**: A user-friendly name used to access the site instead of the IP address.
- **DNS A Record**: Maps the domain (www.foobar.com) to the IP address (8.8.8.8).
- **Nginx (Web Server)**: Manages HTTP requests, serves static files, and proxies dynamic requests.
- **Application Server**: Executes dynamic code and business logic (e.g. user login, data processing).
- **Code Base**: Contains the application source code and static assets.
- **MySQL Database**: Stores structured application data (e.g. users, posts).
- **HTTP Communication**: Protocol used between the browser and server to exchange data (requests/responses).

---

## 4. Architecture Limitations

- **Single Point of Failure (SPOF)**: If the server goes down, the entire site becomes unavailable.
- **Downtime During Maintenance**: Any update, restart, or deployment causes the whole site to be temporarily offline.
- **Limited Scalability**: One server can only handle limited traffic. It cannot easily distribute load or be horizontally scaled.

---
