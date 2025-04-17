# Azure Entra ID Security Lab (Free‑Tier)

A hands‑on, end‑to‑end lab that simulates an enterprise‑grade Identity & Access Management environment in Microsoft Azure.

Built for a cybersecurity portfolio, the project demonstrates how you would design, secure, and monitor a hybrid‐cloud identity platform.

---

## Project Objectives

| # | Goal                                                                  | Why it matters                                |
|---|-----------------------------------------------------------------------|-----------------------------------------------|
| 1 | Stand‑up an Azure Entra ID (formerly Azure AD) tenant                | Foundation for modern cloud identity          |
| 2 | Model a 3‑department company with realistic users, groups & RBAC     | Shows HR, Engineering, Sales segmentation     |
| 3 | Enforce MFA & design Conditional Access policies                     | Baseline security & zero‑trust thinking       |
| 4 | Implement Administrative Units for delegated admin (simulated)       | Demonstrates least‑privilege at scale         |
| 5 | Design a hybrid identity flow with Azure AD Connect (simulated)      | Proves understanding of on‑prem + cloud sync  |
| 6 | Plan log auditing & incident‑response workflows                      | Highlights SOC readiness                      |
| 7 | Document everything with diagrams & screenshots                      | Recruiter‑friendly, interview‑ready portfolio |

---

## High‑Level Architecture

- **On‑Prem Active Directory** → synced via Azure AD Connect
- **Azure Entra ID** acts as the cloud identity plane
- **Cloud apps** (M365, SaaS, Azure services) rely on Entra ID authentication
- **Conditional Access + MFA** enforced at the cloud edge

> *(Architecture is conceptual — no paid services required.)*

---

## Identity Design

| Display Name   | Dept      | Role / Purpose              | Type   |
|----------------|-----------|------------------------------|--------|
| Alice HR       | HR        | HR Manager (privileged)      | Member |
| Sophia Recruiter | HR      | HR Specialist                | Member |
| Bob Developer  | Eng       | Backend Dev                  | Member |
| Lucas Frontend | Eng       | Frontend Dev                 | Member |
| Charlie Intern | Eng       | Engineering Intern           | Member |
| Olivia Sales   | Sales     | Sales Rep                    | Member |
| Mia Manager    | Sales     | Sales Manager (privileged)   | Member |
| Ethan Analyst  | Sales     | Sales Intern                 | Member |
| Ava ITAdmin    | IT        | Global Admin                 | Member |
| Vendor         | –         | External Vendor              | Guest  |


---

## Security Groups

- HR Dept
- Engineering
- Sales
- Managers
- Interns
- Full‑time
- IT Admins
- Guests

---

## Administrative Units (Simulated)

- HR Unit
- Engineering Unit
- Sales Unit

> Scoped role assignments were designed but not applied due to the Premium P1 requirement.

---

## Security Configuration

| Control                | Status                                      | Notes                                         |
|------------------------|---------------------------------------------|-----------------------------------------------|
| MFA                    | Enabled for all users                       | Alice is fully configured                     |
| Conditional Access     | Design only                                 | Documented policies (not enforced):           |
|                        |                                             | - Block sign-ins outside Canada/USA           |
|                        |                                             | - Force password reset on risky logins        |
|                        |                                             | - Restrict interns to 09:00‑18:00 EST         |
| Password Policies      | Azure defaults                              | Strength and expiry documented                |
| Guest Access Hardening | MFA required (design-level)                 | Highlights supply-chain security awareness    |

---

## Monitoring & Incident Response

### Sign-in Logs (Free Tier)
- Location, status, and time-based filters tested
- Screenshots stored in `screenshots/`, even for empty logs
- Use-case example: detect off-hours intern login from foreign IP

### Simulated Incident Flow
1. **Detect**: Anomalous sign-in in logs
2. **Analyze**: User, IP, location, time
3. **Contain**: Disable account / force password reset
4. **Eradicate**: Review CA + MFA settings
5. **Recover**: Re-enable user post-remediation
6. **Lessons Learned**: Update policy & training


---

## Free‑Tier Limitations & Work‑arounds

| Feature                           | Premium? | Mitigation                                |
|-----------------------------------|----------|--------------------------------------------|
| Conditional Access                | Yes (P1) | Policy design documented, not enforced     |
| Scoped roles via Admin Units      | Yes (P1) | Simulated via documentation                |
| Identity Protection risk scoring  | Yes (P2) | Manual log analysis, scenario simulations  |
| Log retention >7 days             | Yes (P1) | Screenshots and exported CSVs retained     |

---

## Repository Layout

```
azure-security-lab/
│
├─ README.md
├─ architecture/
│   └─ hybrid-identity.png
├─ users_groups/
│   ├─ user-structure.md
│   ├─ administrative-units.md
│   └─ rbac-diagram.png
├─ policies/
│   ├─ conditional-access.md
│   └─ security-policy.md
├─ logs/
│   ├─ log-monitoring.md
│   ├─ incident-response.md
│   └─ incident-response.png
└─ screenshots/
    └─ (Azure portal evidence)
```

---

## Key Takeaways

**Cloud‑First + Hybrid Ready**: Simulates full user lifecycle from on-prem to cloud

**Zero‑Trust Mindset**: MFA, Conditional Access design, least-privilege RBAC

**Operational Awareness**: Log auditing, incident playbooks, governance docs

**No Paid Services Needed**: Creative, cost-effective identity engineering

---

## Next Steps (Road‑Map)

Upgrade to Entra ID Premium P1 → enforce Conditional Access & scoped roles

Integrate Defender for Cloud App for advanced analytics

Automate provisioning with Terraform or Bicep

Add Sentinel Workbook to create a SOC-ready dashboard

---

## Skills Demonstrated

- Azure Active Directory (Entra ID)
- IAM Design (Users, Groups, Roles)
- Conditional Access & MFA Enforcement
- Administrative Units for delegated management
- Azure Security Best Practices
- Documentation & GitHub-based portfolio development

