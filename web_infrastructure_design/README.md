File: 0-simple_web_stack
Scenario:
A user wants to visit www.foobar.com.
How it works:
The user types www.foobar.com in their browser.
DNS resolves the domain using a DNS A record that maps www.foobar.com to IP address 8.8.8.8.
The request is sent to the server at 8.8.8.8.

Server Components:
Web Server (Nginx): Accepts the HTTP request and forwards it to the application server.
Application Server: Runs the website's backend code (e.g., PHP, Python).
Application Files: Codebase that contains business logic and serves dynamic content.
MySQL Database: Stores persistent data (e.g., user data, blog posts).

Communication Protocol: The server and user’s computer communicate via HTTP.
Key Concepts:
What is a server? A physical or virtual computer that runs services to serve client requests.
Domain Name: A human-readable address mapped to a server’s IP.
DNS Record Type: www is a subdomain using an A record to map to the server IP.
Web Server Role: Handles HTTP requests and forwards them.
App Server Role: Processes logic and interacts with the database.
Database Role: Stores and retrieves structured data.

Issues:
Single Point of Failure (SPOF): If the server fails, the website is down.
Downtime During Maintenance: Restarting Nginx or updating code causes service interruption.
Scalability: Can’t handle high traffic loads.

File: 1-distributed_web_infrastructure
Scenario:
A more resilient infrastructure with load balancing and two web servers.

Components:
HAProxy Load Balancer: Distributes traffic to the backend servers. Uses a Round-Robin algorithm (rotates requests evenly).
Active-Active setup: Both backend servers are active and handle traffic simultaneously.
2 Web Servers (with same stack): Nginx + App Server + App Files + MySQL

Database Setup:
Primary-Replica (Master-Slave) configuration:
Primary Node: Accepts writes and reads.
Replica Node: Only used for read queries to reduce load on the primary.

Purpose of Additional Components:
HAProxy: Increases availability and balances traffic.
Multiple Servers: Improves redundancy and scalability.
Primary-Replica DB: Enables load distribution for queries and backups.

Issues:

SPOF: HAProxy itself can be a single point of failure.
No Firewalls/HTTPS: Vulnerable to attacks.
No Monitoring: No visibility into server health.

File: 2-secured_and_monitored_web_infrastructure
Added Components:

3 Firewalls:
One on each server to filter traffic (web, app, db).
Only allow necessary ports (e.g., 80, 443, 3306).

1 SSL Certificate:
Encrypts traffic between client and server using HTTPS.
Improves security and privacy.

3 Monitoring Clients:
Installed on each server.
Send metrics to a centralized monitoring service like SumoLogic.
Track metrics like CPU usage, response time, QPS (Queries per Second).

Purpose:
Firewalls: Prevent unauthorized access to servers.
HTTPS: Encrypts data in transit to prevent eavesdropping.
Monitoring: Alerts admins to failures or unusual behavior.
Monitoring QPS: Collect Nginx logs.
Use the monitoring tool to parse logs and extract QPS metrics.

Issues:
SSL Termination at Load Balancer:
Traffic between LB and backend may be unencrypted unless re-encrypted.
One MySQL write node: Still a bottleneck and SPOF.
Identical Components on All Servers: Inefficient and complicates scaling.

File: 3-scale_up
Goal:
A modular and scalable infrastructure.

New Components:
New HAProxy (Clustered with previous one): Increases high availability of load balancing. If one fails, the other takes over.

Dedicated Servers:
1 Web Server (Nginx)
1 Application Server
1 Database Server (MySQL)

Purpose of Splitting:
Web Server: Handles static files, reduces load on other components.
App Server: Dedicated to processing logic, better performance.
DB Server: Centralizes and optimizes database management.

Why Add Each:
Improves performance.
Easier to maintain and scale.
Better resource utilization.


