Simple web stack


A user wants to access your website by entering www.foobar.com into their browser. Below is the step-by-step flow of how the web infrastructure processes the request:

1. User's Request

    User Action: The user types www.foobar.com into their browser and presses Enter.
    DNS Resolution:
        The browser sends a DNS query to resolve www.foobar.com.
        The DNS server responds with the server's IP address: 8.8.8.8.

2. Server Components

Infrastructure Design:

    Web Server (Nginx):
        Acts as the entry point for all incoming HTTP/HTTPS requests.
        It listens on port 80 for HTTP and port 443 for HTTPS.
        Nginx is configured as a reverse proxy to forward requests to the application server.

    Application Server:
        Hosts the backend logic for the website (e.g., written in Python/Django, Node.js, PHP, etc.).
        Communicates with the web server (Nginx) to process requests.

    Application Files:
        The codebase is stored on the server (e.g., HTML, CSS, JavaScript for frontend, backend logic files, etc.).
        The application server reads these files to generate responses.

    Database (MySQL):
        Stores website data such as user information, blog posts, or product details.
        The application server queries the database to fetch or update data as required.

3. Flow of a Request

    Step 1: DNS Lookup
        The user's browser resolves www.foobar.com to 8.8.8.8.

    Step 2: Web Server (Nginx)
        The browser sends an HTTP/HTTPS request to 8.8.8.8.
        Nginx receives the request and forwards it to the application server.

    Step 3: Application Server
        The application server processes the request by executing the backend logic.
        It may fetch data from the MySQL database if needed.

    Step 4: Database (MySQL)
        The application server queries the MySQL database for required data.
        The database responds with the requested data.

    Step 5: Response
        The application server uses the application files (codebase) to generate the appropriate response (HTML, JSON, etc.).
        The response is sent back to Nginx.
        Nginx forwards the response to the user's browser.

    Step 6: User's Browser
        The user's browser renders the response, displaying the website.

SPOF (Single Point of Failure):

    Issue: Since the entire infrastructure relies on a single server, if this server fails (e.g., due to hardware issues, power failure, or network outage), the entire website becomes inaccessible.
    Impact: Users cannot access the website until the issue is resolved, leading to downtime and potential revenue loss.

Downtime for Maintenance:

    Issue: When performing maintenance tasks such as deploying new code or restarting the web server (Apache or Nginx), the website is temporarily unavailable.
    Impact: Users experience disruptions or errors when trying to access the website during this period.

Scalability:

    Issue: A single server cannot handle high volumes of traffic effectively. If there is a sudden surge in traffic, the server may become overloaded, leading to slow performance or a crash.
    Impact: Poor user experience and potential loss of visitors.

Link to JPG: https://imgur.com/a/5SwNDHM
