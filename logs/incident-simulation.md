# Incident Simulation & Response Playbook


This document walks through **two simulated identity‑based attack scenarios** inside the Azure Entra ID lab.  
Although no live traffic exists in the free‑tier environment, each step mirrors real SOC procedures and demonstrates how I would **detect, contain, and eradicate** threats.

---

## 1  SOC Playbook Structure
| Phase | Action | Tooling (Free Tier) |
|-------|--------|--------------------|
| **Preparation** | Baseline MFA, groups, audit logging enabled | Azure Portal |
| **Detection** | Monitor **Sign‑in Logs** & email alerts | Entra ID → Monitoring |
| **Analysis** | Pivot on user, IP, timestamp, MFA result | Sign‑in log filters |
| **Containment** | Disable account / revoke sessions | Entra ID user blade |
| **Eradication** | Reset password, enforce MFA, review CA | Per‑user MFA portal |
| **Recovery** | Re‑enable account, notify user, close ticket | ITSM / ticketing |
| **Lessons Learned** | Update policy, add detections, share report | Confluence / README |

---

## 2  Scenario A – Compromised Intern Account (Off‑Hours Login)

| Item | Detail |
|------|--------|
| **User** | `charlie@…` (Engineering Intern) |
| **Event** | Failed sign‑in at **03:14 AM EST** from **Romania** |
| **Detection Method** | Manual filter: *Status = Failure · Location ≠ CA/US · User = Interns* |
| **Risk** | Possible credential stuffing or password spray |

### Response Steps
1. **Contain** – Disable `Charlie` account immediately.  
2. **Investigate** – Check *Audit Logs* for recent password resets or role changes.  
3. **Eradicate** – Force password reset + require MFA at next sign‑in.  
4. **Recover** – Re‑enable account after intern verifies device hygiene.  
5. **Lessons Learned** – Re‑prioritise planned Conditional Access rule:  
   *“Block Intern group outside 09:00–18:00 EST & outside CA/USA.”*  

---

## 3  Scenario B – Brute‑Force on Guest Vendor

| Item | Detail |
|------|--------|
| **User** | `vendor@ext.com` (Guest) |
| **Event** | 5 failed sign‑ins within 2 minutes from 3 IP ranges |
| **Detection Method** | Sign‑in log filter: *User Type = Guest · Status = Failure · Last 24 h* |
| **Risk** | Credential leak of external partner account |

### Response Steps
1. **Contain** – Permanently **block sign‑in** for `vendor@ext.com`.  
2. **Notify** – Email vendor security POC to rotate credentials.  
3. **Eradicate** – Review any *app permissions* the guest may hold.  
4. **Hardening** – Document a new policy: *“Guests must register MFA within 24 h or be auto‑disabled.”*  

---

## 4  Log Evidence (Screenshots Stored)

| Screenshot | Description |
|------------|-------------|
| `Logs.png` | Baseline log view (free tier, no real traffic) |



---

## 5  Detection Engineering Road‑Map

| Stage | Upgrade | Benefit |
|-------|---------|---------|
| **Short Term** | Export sign‑in logs to CSV, build KQL queries locally | Ad‑hoc threat hunting |
| **Mid Term** | Connect **Log Analytics Workspace** (cost‑controlled) | Alerts & dashboards |
| **Long Term** | Deploy **Microsoft Sentinel** with Identity workbook |  Fusion ML, SOAR playbooks |


---

## 6  Key Takeaways

- Even without paid features, **manual log review** and **well‑defined playbooks** provide strong security posture.
- **Proactive Conditional Access design** (documented earlier) would automate both scenarios.
- The exercise highlights my ability to **think like a SOC analyst**, craft incident workflows, and translate findings into actionable policy.

---
