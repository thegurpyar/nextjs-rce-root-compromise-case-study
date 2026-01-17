# Incident Timeline (Reconstructed)

> Times are approximate and based on log correlation.

---

## Phase 1: Exposure
- Server deployed with public IP
- Outdated Next.js application running
- Application executed as `ubuntu` user
- Passwordless sudo enabled by default

---

## Phase 2: Discovery
- Automated scanners detected HTTP service
- Next.js fingerprint identified
- Known exploit patterns attempted

---

## Phase 3: Initial Compromise (RCE)
Attacker achieved server-side command execution via a vulnerable or misconfigured Next.js endpoint.

**Observed probe commands:**
```bash
whoami
uname -a
id
cat /etc/passwd
