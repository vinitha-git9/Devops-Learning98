Web Server:

-> A web server is the software ( sometimes a hardware) that
  .stores website files(html,css,javascript etc)
  .serves them to users over the internet when requested by the browser.
  .hnadles request using HTTP or HTTPS protocol
 
Hardware: A physical or virtual machine that stores web server software and website data (HTML, CSS, JS, images, etc.).

Software: The web server application that handles HTTP requests. Popular examples include:
.> Nginx
.>Apache
.>Microsoft IIS
.>Litespeed

When a user accesses a website via a browser, the browser sends an HTTP(S) request to the web server. 
The server processes the request and returns the appropriate response (e.g., a web page).

HTTP vs HTTPS:

HTTP: Data sent in plaintext. Vulnerable to eavesdropping and man-in-the-middle attacks.

HTTPS (HTTP Secure): Encrypts data using TLS (Transport Layer Security). Ensures:
It encrypt the communication between the browser and the server to protect against:
Eavesdropping
Data tampering
Man-in-the-middle attacks

How HTTPS Works (Simplified)

Browser connects to the server via HTTPS.
Server presents its SSL/TLS certificate to prove its identity.
Browser verifies the certificate using a Certificate Authority (CA).
TLS handshake occurs:
They agree on encryption methods.
They exchange keys securely.
Encrypted communication begins.

🔹 Why Are Web Servers Required?

1.Host websites and appilcation(Web servers store your website files (HTML, CSS, JS, images, etc.).)
2.serve content over the web(This is usually done via HTTP or HTTPS protocols.)
3.handle user requests(It then sends the correct data back to the user.)
4.supports security and authentication(With HTTPS, web servers ensure secure, encrypted communication.)
5.Enable online service(simple blogs to complex apps like online shopping, social media, or email.)
6.serve APi's and backend logic(Web servers often run backend scripts (like PHP, Python, Node.js) to handle database queries, form submissions, etc.)


