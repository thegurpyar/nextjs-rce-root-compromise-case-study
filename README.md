# RCE to Root: Cryptominer Compromise on AWS Lightsail (Next.js Case Study)

## Overview
In January 2026, a production Ubuntu server hosted on AWS Lightsail was compromised and used to run a cryptocurrency miner (xmrig / Monero).

The attack was **opportunistic**, not targeted, and resulted from a combination of:
- An outdated Next.js application
- An internet-facing deployment
- The application running as a sudo-enabled user

This repository documents the **attack chain**, **evidence**, **root cause analysis**, and **preventive measures**, based on real incident response findings.

> ⚠️ This report is anonymized and shared strictly for educational and defensive security purposes.

---

## Executive Summary
- Outdated Next.js application exposed server-side RCE
- Application ran as default `ubuntu` user with passwordless sudo
- RCE led directly to full root compromise
- Persistence mechanisms were installed
- xmrig Monero miner consumed ~100% CPU
- Reboots did not remove the compromise

No SSH brute-force, stolen AWS credentials, or kernel exploits were involved.

---

## Environment Details

| Component | Details |
|--------|--------|
| Cloud Provider | AWS Lightsail |
| OS | Ubuntu (official image) |
| Default User | `ubuntu` (passwordless sudo) |
| Application | Next.js (outdated) |
| Runtime | Node.js |
| Exposure | Public IP (80 / 443 / 3000) |
| Security Controls | No WAF, no isolation |

**Note:**  
Lightsail Ubuntu images retain the same default sudo configuration as standard EC2 images unless explicitly hardened.

---

## High-Level Attack Chain

Internet Scan
→ Next.js Server-Side RCE
→ Node.js Process (ubuntu)
→ sudo -i
→ Root Access
→ Persistence (systemd + cron)
→ xmrig Cryptominer


---

## Root Cause Analysis

### Primary Causes
- Outdated Next.js version with server-side execution risks
- Application running as a sudo-enabled user

### Contributing Factors
- Direct internet exposure
- No WAF or request filtering
- No process isolation
- No runtime monitoring

---

## Lessons Learned
- App-level RCE equals root compromise when sudo is available
- Default cloud images favor convenience over security
- Cryptominers hide in plain sight
- Rebooting does not remove persistence

---

## Preventive Measures

### Immediate
- Instance terminated and rebuilt
- All secrets rotated

### Long-Term
- Dedicated non-sudo application user
- Minimal permissions for web apps
- Regular updates of Next.js / React / Node.js
- Disable SSH where possible or harden it
- Restrict inbound ports
- Continuous dependency audits

---

## Responsible Use
This case study is shared for defensive security awareness only.  
Do not use this information for unauthorized access or exploitation.
