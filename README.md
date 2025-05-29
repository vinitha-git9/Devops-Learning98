# 🌐 Web Server & App Server Guide

## 📡 Web Server

A web server is a system that delivers web content (like websites, images, and videos) to users over the internet.

### Components of a Web Server:

- **Request Handler:** Apache HTTP, Nginx, Microsoft IIS, LiteSpeed  
- **Interpreter:** PHP, Java, Perl  
- **Storage:** Oracle, MySQL  

### Request Flow:

Client → Browser → Data → Encrypt/Decrypt → Session → Segments → Packets → Frames → Bits → Network → Webserver
→ Apache/Nginx handles request → Fetch index file → Interpret file → Query database → Respond to client


---

## 🌐 HTTP vs HTTPS

- **HTTP:** Data sent in plaintext. Vulnerable to attacks.
- **HTTPS:** Encrypted version of HTTP using SSL/TLS.

### How They Work in a Web Server:

1. User enters URL → browser sends HTTP/HTTPS request  
2. Web server listens on port `80` (HTTP) or `443` (HTTPS)  
3. It determines how to respond: static file, run script, access DB  
4. If HTTPS is used → SSL/TLS handshake ensures encryption  

---

## 🅰️ Apache

Apache is a widely used open-source web server.

### 🔧 What Apache Does:

- Serves content like HTML, images, and videos  
- Handles dynamic content (PHP, Python, etc.) via modules  
- Supports virtual hosting  

### 🔌 Useful Modules:

- `mod_ssl` – Enables HTTPS  
- `mod_rewrite` – Allows URL rewriting  
- `mod_php` – PHP processing  

### 🛠 Config Files:

- `/etc/httpd/conf/httpd.conf` (Red Hat/CentOS)  
- `/etc/apache2/apache2.conf` (Ubuntu/Debian)  

---

## ⚙️ NGINX

NGINX (pronounced "engine-x") is a high-performance web server and reverse proxy.

### 💼 What NGINX Can Do:

| Function             | Description                                                   |
|----------------------|---------------------------------------------------------------|
| 🌍 Web Server        | Serves static content like HTML, images                       |
| 🔁 Reverse Proxy     | Forwards client requests to backend servers                   |
| ⚖️ Load Balancer     | Distributes traffic across multiple servers                   |
| 🗂️ Static Server     | Efficient for static files                                     |
| 🔐 SSL Termination   | Manages secure HTTPS connections                              |

### 🧠 How It Works:

Browser
↓
NGINX (port 80/443)
↓
App Server (e.g., Node.js)


### 📁 Configuration:

- Main config: `/etc/nginx/nginx.conf`
- Site config: `/etc/nginx/sites-available/your-site`

### 🔍 Used By:

Netflix, GitHub, Dropbox, Instagram, WordPress.com

---

## 🧠 Application Server

Runs backend application logic like Python, Node.js, Java, etc.

### 🔄 Workflow:

User → NGINX → App Server → DB → App Server → NGINX → Browser

### 📊 Architecture Diagram:

Browser
↓
NGINX (Web Server)
↓
App Server (Flask, Node.js, etc.)
↓
Database (MySQL, MongoDB)


---

## 🔒 SSL Certificates

SSL (Secure Sockets Layer, now TLS) encrypts communication between server and browser.

### ✅ Benefits:

- Encrypts traffic
- Validates website identity

### 💡 Indicators:

- With SSL: `https://example.com` 🔒
- Without SSL: `http://example.com` ❌ Not secure

---

## 📁 Hosting a Static Site with NGINX

### Setup:

```bash
cd /var/www/html
mkdir mywebsite
nano index.html

<!DOCTYPE html>
<html>
<head><title>My Static Website</title></head>
<body><h1>Hello from NGINX static site!</h1></body>
</html>

sudo chmod -R 755 /var/www/html/mywebsite

Create NGINX Server Block:
# /etc/nginx/sites-available/mywebsite

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

Visit http://localhost to see your static site.


🛠 Monitoring with Monit

Configure Monit:

# /etc/monit/monitrc/conf-enabled/nginx

check process nginx with pidfile /run/nginx.pid
  start program = "/usr/sbin/service nginx start"
  stop program  = "/usr/sbin/service nginx stop"
  if failed port 80 protocol http then restart
  if 5 restarts within 5 cycles then timeout

🧩 Monitoring with Supervisor (Python App Example)

Example App:
# /home/vboxuser/pyapp/myapp.py
import time

while True:
    print("My Python app is running...")
    time.sleep(5)

Supervisor Config:
# /etc/supervisor/conf.d/pyapp.conf

command=/usr/bin/python3 /home/vboxuser/pyapp/myapp.py
autostart=true
autorestart=true
stdout_logfile=/var/log/pyapp.out.log
stderr_logfile=/var/log/pyapp.err.log


sudo supervisorctl reread
sudo supervisorctl update
sudo supervisorctl start myapp
sudo supervisorctl status

📘 Web Server vs Application Server


| Feature        | Web Server                        | Application Server                |
| -------------- | --------------------------------- | --------------------------------- |
| Main Job       | Serve static files (HTML/CSS/JS)  | Run backend code                  |
| Executes Code? | ❌ No                              | ✅ Yes                             |
| Serves Static? | ✅ Yes                             | ❌ Not ideal                       |
| Talks to DB?   | ❌ No                              | ✅ Yes                             |
| Examples       | Apache, NGINX                     | Gunicorn, Node.js, Tomcat         |
| Use Case       | Host static site or reverse proxy | Process logic (e.g., login, APIs) |

📝 Summary

Webserver – Delivers static content over HTTP/HTTPS

Apache – Powerful open-source web server

Nginx – Fast, modern web server and reverse proxy

App server – Runs backend code and dynamic responses

HTTP/HTTPS – Web communication protocols (HTTPS is secure)

SSL certs – Enable secure, encrypted connections over HTTPS
