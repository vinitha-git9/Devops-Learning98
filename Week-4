
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

Installation of Monit and Supervisor:

sudo apt install monit -y
sudo systemctl enable monit
sudo systemctl start monit
monit -V
sudo nano /etc/monit/monitrc

set httpd port 2812 and
    use address localhost
    allow localhost

sudo monit reload


Supervisor:
sudo apt install supervisor -y
sudo systemctl enable supervisor
sudo systemctl start supervisor
supervisord -v
sudo nano /etc/supervisor/conf.d/myapp.conf


[program:myapp]
command=/usr/bin/python3 /opt/myapp/app.py
autostart=true
autorestart=true
stderr_logfile=/var/log/myapp.err.log
stdout_logfile=/var/log/myapp.out.log

sudo supervisorctl reread
sudo supervisorctl update
