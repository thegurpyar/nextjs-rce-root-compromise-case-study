# RCE to Root: Cryptominer Compromise on AWS Lightsail (Next.js Case Study)

## Overview
In January 2026, a production Ubuntu server hosted on AWS Lightsail was compromised and used to run a cryptocurrency miner (xmrig / Monero).  
The attack was opportunistic, not targeted, and resulted from a chain of common misconfigurations combined with an outdated web framework.

This repository documents the **full attack chain**, **evidence**, **root cause analysis**, and **preventive measures**, based on real incident response findings.

> ⚠️ This report is anonymized and shared strictly for educational and defensive security purposes.

---

## Executive Summary
- Outdated Next.js application exposed a server-side execution vulnerability
- Application ran as default `ubuntu` user with passwordless sudo
- Remote Code Execution (RCE) led directly to full root compromise
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

