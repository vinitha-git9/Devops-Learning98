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
