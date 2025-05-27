Web Server:
A web server is a system that delivers web content (like websites, images, and videos) to users over the internet.

Webserver components:

Request handler: Apache HTTP, Nginx, Microsoft IIS, litespeed
Intrepeter: PHP, java,perl
Stroage: Oracle, Mysql

Client ---> browser ---> data ---> encryption /decryption ---> session occurs ---> data convert to segments ---> segments to packet --->then converted to frame ---> then converted to bits ---> sent as signals over the network --->  connected to webserver -- request is handled by apache/Nginx -- fetch the indexfile from filestorage -- then interpret the file -- > fetch the data from database ---->  delivered the data to client.

HTTP/HTTPS:

HTTP: Data sent in plaintext. Vulnerable to eavesdropping and man-in-the-middle attacks.
HTTPS stands for HyperText Transfer Protocol Secure. It is the secure version of HTTP, the protocol used for transferring data over the web

How HTTP/HTTPS Fit Into a Web Server:

User types a URL or clicks a link ----> The browser sends an HTTP or HTTPS request to the web server ---> Web Server Software Receives Request 
---- The web server (like Apache or Nginx) listens on:Port 80 for HTTP,Port 443 for HTTPS ----> It processes the request and decides:
What file or script to serve --> Whether to run server-side code (e.g., PHP)----> Whether to communicate with a database

3. If Using HTTPS (Secure)
The server and browser perform an SSL/TLS handshake:

Apache (short for Apache HTTP Server):
is one of the most widely used open-source web server software applications in the world. It allows you to host websites and web applications on the internet.

🔧 What Apache Does
...>Receives requests from clients (usually web browsers)
...>Serves content like HTML files, images, and videos
....>Can run dynamic content (PHP, Python, etc.) using modules
.....>Supports virtual hosting (multiple websites on one server)

Apache Modules:
mod_ssl – Enables HTTPS support
mod_rewrite – Allows URL rewriting
mod_php – Enables PHP processing

Apache Configuration Files:
/etc/httpd/conf/httpd.conf (Red Hat/CentOS)
/etc/apache2/apache2.conf (Ubuntu/Debian)

Nginx:

NGINX (pronounced "engine-x") is:
A high-performance web server that can also act as a reverse proxy, load balancer, and HTTP cache.
It’s widely used by websites to serve content quickly, securely, and reliably.

What Nginx do?
| Function               | Explanation                                                         |
| ---------------------- | ------------------------------------------------------------------- |
| 🌍 **Web Server**      | Shows websites to users (serves HTML, CSS, images, etc.)            |
| 🔁 **Reverse Proxy**   | Passes client requests to backend servers (like Node.js, PHP, etc.) |
| ⚖️ **Load Balancer**   | Spreads traffic across multiple servers to avoid overload           |
| 🗂️ **Static Server**  | Efficiently serves static files (images, HTML)                      |
| 🔐 **SSL Termination** | Handles HTTPS connections (secure)                                  |

How Nginx works:

User’s Browser
     ↓
   NGINX (Port 80/443)
     ↓
  Your App (e.g. Node.js on Port 3000)

NGINX Configuration Basics:
Main config file (Linux):
📍 /etc/nginx/nginx.conf
Site-specific config:
📍 /etc/nginx/sites-available/your-site+

🔍 Where NGINX Is Used
Netflix
GitHub
Dropbox
WordPress.com
Instagram

An Application Server is a program that runs your web application code (like Python, Node.js, PHP, Java, etc.) and handles dynamic content — like logins, form submissions, or database queries.
It does not serve static files like images or HTML pages — that’s what NGINX does best.

User visits https://example.com/login
NGINX receives the request
NGINX sends the request to the app server (on port 3000, for example)
The app server processes the login (checks username/password from the database)
Sends back a response to NGINX
NGINX returns the response to the user's browser

Diagram:

Browser (User)
     ↓
NGINX (Reverse Proxy & Web Server)
     ↓
App Server (e.g., Node.js, Flask, PHP)
     ↓
Database (e.g., MySQL, MongoDB)

The App Server runs your actual application.
NGINX sits in front of it and handles the traffic, security, and performance.


SSL stands for Secure Sockets Layer (now technically called TLS, but most people still say "SSL").

An SSL certificate is a digital certificate that:

✅ Confirms your website’s identity
✅ Encrypts the data sent between the browser and your server

 What It Looks Like
With SSL (HTTPS):
https://example.com 🔒 Lock icon in browser

Without SSL (HTTP):
http://example.com ❌ "Not secure" warning


Install and config Nginx to run a static web page:

cd /var/www/html  --- mkdir mywebsite
nano index.html

<!DOCTYPE html>
<html>
<head>
  <title>My Static Website</title>
</head>
<body>
  <h1>Hello from NGINX static site!</h1>
</body>
</html>

sudo chmod -R 755 /var/www/html/mywebsite

Create NGINX Server Block (Config):

sudo nano /etc/nginx/sites-available/mywebsite
server {
    listen 80;
    server_name localhost;

    root /var/www/mywebsite;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}

sudo ln -s /etc/nginx/sites-available/mywebsite /etc/nginx/sites-enabled/

sudo nginx -t
sudo systemctl reload nginx


On local machine:
http://localhost

O/P:
Hello from NGINX static site!
