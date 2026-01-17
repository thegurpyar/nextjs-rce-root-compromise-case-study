# Incident Timeline (Reconstructed)

> Times are approximate and based on log correlation.

---

## Phase 1: Exposure
- Server deployed with public IP
- Outdated Next.js application running
- Application executed as `ubuntu`
- Passwordless sudo enabled by default

---

## Phase 2: Discovery
- Automated scanners detected HTTP service
- Next.js fingerprint identified
- Known exploit patterns attempted

---

## Phase 3: Initial Compromise (RCE)
Attacker achieved server-side command execution.

Observed probe commands:
```bash
whoami
uname -a
id
cat /etc/passwd
```

## Phase 4: Privilege Escalation

Attacker discovered sudo access

Executed:
```bash
sudo -i
```

Root shell obtained immediately

## Phase 5: Persistence Setup

Persistence mechanisms added:

systemd service

root cron @reboot job

hidden binaries in system paths

## Phase 6: Payload Deployment

xmrig miner downloaded and extracted

Binary placed inside application directory

Miner connected to Monero pool

CPU usage reached ~100%

## Phase 7: Detection & Response

Performance degradation noticed

Suspicious processes identified

Persistence confirmed

Instance terminated and rebuilt
