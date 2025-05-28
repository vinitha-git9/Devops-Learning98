A daemon is just a background program that provides services or watches your system. 
Tools like Monit, Supervisor, cron, or sshd all run as daemons.

Difference b/w Monit and Supervisor:

| Feature            | **Monit**                            | **Supervisor**                         |
| ------------------ | ------------------------------------ | -------------------------------------- |
| **Purpose**        | System monitoring and self-healing   | Process management for apps/scripts    |
| **Best for**       | System services (e.g., Nginx, MySQL) | App processes (e.g., Python, Node.js)  |
| **Monitoring**     | Yes (CPU, memory, file checks, etc.) | No (only checks if process is running) |
| **Auto-Restart**   | ✅ Yes                                | ✅ Yes                                  |
| **Alerting**       | ✅ Built-in email alerts              | ❌ Requires custom scripts              |
| **Web Interface**  | ✅ Yes (via port 2812)                | ❌ No (unless extended with plugins)    |
| **Resource Usage** | Lightweight                          | Lightweight                            |
| **Config Style**   | Custom declarative syntax            | INI file format                        |

Installed Ubuntu

Installation of Monit:

sudo yum install epel release
sudo yum install monit -y
sudo systemctl enable monit
sudo systemctl status monit
monit -v

Configuration:

To monit NGINX service:

cd /etc/monit
nano monitrc

set httpd port 2812 and
    use address 127.0.0.1
    #allow localhost
allow admin:monit

Open local web browser--> enter http://127.0.0.0:2812

check process nginx with pidfile /run/nginx.pid
start prpgram= "/usr/sbin/service nginx start"
stop program = "/usr/sbin/servive nginx stop"
if failed 127.0.0.1 port 80 protocol http for 3 cycles then restart

set mailserver smtp.gmail.com port 587
username = "vinitharaja@gmail.com" password= "app password"
using tls

sudo monit -t
sudo monit reload
sudo monit status

To find the Nginx status:
systemctl status nginx

To sent alert to mail:
systemctl stop nginx

check mail

Open local web browser--> enter http://127.0.0.0:2812

SUPERVISOR:

python app install:
cd /
apt install python3

mkdir ~/pyapp
cd ~/pyapp
nano myapp.py

# myapp.py
import time

while True:
    print("Python app is running...")
    time.sleep(5)

Install nodeapp also and create index.fs
 
sudo nano /etc/supervisor/conf.d/pyapp.conf

[program:pyapp]
command=/usr/bin/python3 /home/vboxuser/pyapp/myapp.py
autostart=true
autorestart=true
stdout_logfile=/var/log/pyapp.out.log
stderr_logfile=/var/log/pyapp.err.log

sudo nano /etc/supervisor/conf.d/nodeapp.conf

[program:nodeapp]
command=/usr/bin/node /nodeapp/index.js
autostart=true
autorestart=true
stderr_logfile=/var/log/nodeapp/nodeapp.err.log
stdout_logfile=/var/log/nodeapp/nodeapp.out.log

sudo apt install supervisor -y
sudo systemctl enable supervisor
sudo systemctl start supervisor
supervisord -v

sudo supervisorctl reread
sudo supervisorctl update


sudo supervisorctl status pyapp
sudo supervisorctl status nodeapp

Graceful shutdown:
To implement graceful shutdown in a Python app (especially one run by Supervisor), you need to handle termination signals like SIGTERM and SIGINT. This lets your app clean up resources before exiting.


Graceful Shutdown in Python:

cd /etc/pyapp
nano app.py
 
import time
import signal
import sys

running = True

def handle_exit(signum, frame):
    global running
    print("\nReceived termination signal. Cleaning up...")
    running = False

# Handle Ctrl+C and Supervisor stop
signal.signal(signal.SIGINT, handle_exit)
signal.signal(signal.SIGTERM, handle_exit)

print("Python app started.")
while running:
    print("Python app is running...")
    time.sleep(5)

print("Shutdown complete. Exiting.")

Manual run:
python3 app.py

Press Ctrl+C → You’ll see:
Received termination signal. Cleaning up...
Shutdown complete. Exiting.

✅ Under Supervisor
sudo supervisorctl stop pyapp

EVENT LISTENER:
In Python, event listeners are used to respond to specific events, such as user input, network activity, signals, or other triggers.
Python doesn’t have a built-in event system like JavaScript, but you can implement event-driven behavior using libraries or your own custom logic.

cd /etc/pyapp
nano app.py

✅ 1. Simple Custom Event Listener (Basic Pattern)

class EventEmitter:
    def __init__(self):
        self.listeners = {}

    def on(self, event, callback):
        if event not in self.listeners:
            self.listeners[event] = []
        self.listeners[event].append(callback)

    def emit(self, event, *args, **kwargs):
        for callback in self.listeners.get(event, []):
            callback(*args, **kwargs)

# Example usage
emitter = EventEmitter()

def on_shutdown():
    print("Shutting down...")

emitter.on('shutdown', on_shutdown)

# Later in your code
emitter.emit('shutdown')

run: Python3 app.py

shutting down
| Feature                | **Systemd**                       | **Supervisor**                   | **Monit**                      |
| ---------------------- | --------------------------------- | -------------------------------- | ------------------------------ |
| Primary Use            | Init system, service management   | Process supervision              | Process & system monitoring    |
| Auto-Restart           | ✅ Yes                             | ✅ Yes                            | ✅ Yes                          |
| Process Monitoring     | 🚫 (basic only)                   | ✅ Good                           | ✅ Advanced                     |
| System Resource Checks | ❌                                 | ❌                                | ✅ (CPU, RAM, disk, etc.)       |
| Email Alerts           | ❌                                 | ❌                                | ✅ Yes                          |
| Web Interface          | ❌                                 | ❌                                | ✅ Yes                          |
| Logs                   | `journalctl`                      | stdout/stderr to log files       | Custom log paths               |
| Configuration Style    | Declarative `.service` files      | INI-style `.conf` files          | Custom `.monitrc` or snippets  |
| Daemon Required        | Yes (part of OS)                  | Yes (supervisord)                | Yes (monit daemon)             |
| Boot Management        | ✅ Excellent (`enable`, `disable`) | ❌ (manual or via cron/systemd)   | ❌ (needs to be added manually) |
| Use Case               | OS services, system boot          | Python, Node.js, background apps | Monitoring and auto-healing    |

Configure & Monitor a process with Supervisor/Monit and start this process at system startup:

sudo nano /etc/monit/conf-enabled/myapp

check process myapp
    matching "app.py"
    start program = "/usr/bin/python3 /home/ubuntu/myapp/app.py"
    stop program = "/usr/bin/pkill -f /home/ubuntu/myapp/app.py"
    if not exist then restart

Configure Supervisor/Monit to send  mail alerts on higher resource usage (CPU, Memory, Disk):

cd /etc/monit
nano monitrc

set daemon 60            # Check every 60 seconds
set logfile /var/log/monit.log

set mailserver smtp.gmail.com port 587
    username "your_email@gmail.com" password "your_app_password"
    using tlsv12

set alert your_email@gmail.com

check system localhost
    if loadavg (1min) > 4 then alert
    if memory usage > 75% then alert
    if cpu usage (user) > 70% then alert

check filesystem rootfs with path /
    if space usage > 85% then alert

set httpd port 2812 and
    use address localhost
    allow localhost

monit -t
monit reload
monit status
