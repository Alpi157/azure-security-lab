# SecureOrg Identity & Access Security Policy  
> **File:** `policies/security-policy.md`  
> **Version:** 1.0 | **Status:** Draft ( portfolio) | **Last Updated:** 2025‑04‑17

---

## 1  Purpose
To define the minimum security requirements for identity lifecycle management, authentication, authorization, and monitoring in SecureOrg’s hybrid‑cloud environment powered by Microsoft Azure Entra ID.

---

## 2  Scope
| In‑Scope | Out‑of‑Scope |
|----------|--------------|
|  All Azure Entra ID cloud identities (users & guests) | Physical security |
|  On‑prem Active Directory objects (synced) | OT / IoT devices |
|  SaaS & Azure applications federated to Entra ID | Third‑party IdPs |

---

## 3  Roles & Responsibilities
| Role | Responsibility |
|------|----------------|
| **IT Admins** | Tenant configuration, break‑glass accounts, AD Connect |
| **HR Manager** | Joiners/Movers/Leavers updates for HR Unit |
| **Department Managers** | Approve access requests within their Admin Unit |
| **Security Team (SOC)** | Monitor logs, triage incidents, enforce policy |
| **All Users** | Maintain credential secrecy, complete MFA prompts |

---

## 4  Policy Statements

### 4.1  Authentication
1. **Multi‑Factor Authentication** is mandatory for all human and guest accounts.  
2. Break‑glass accounts (max 2) are exempt from MFA but protected by 64‑char random passwords stored offline.

### 4.2  Password Controls
| Control | Setting |
|---------|---------|
| Minimum Length | 14 characters |
| Complexity  | Upper, lower, number, symbol |
| Expiry      | 180 days |
| History     | 24 passwords remembered |
| Lockout     | 10 failed attempts → 10 min lock |

### 4.3  Authorization & RBAC
- Access is granted via Security Groups; direct user assignments to apps are prohibited.  
- Administrative Units segment HR, Engineering, and Sales. Scoped roles limit admins to their own unit (requires P1; currently documented).  
- **Principle of Least Privilege**: elevated roles (Global Admin, User Admin) issued only via written approval and reviewed quarterly.

### 4.4  Guest & Vendor Access
All guest accounts must use **MFA** and reside in the **Guests** group.  
Access is time‑boxed to **90 days**; extension requires sponsor approval.

### 4.5  Conditional Access (Design Phase)
Policies P‑01 … P‑04 (see `conditional-access.md`) shall be enforced upon subscription to Azure AD Premium P1.

### 4.6  Monitoring & Logging
- Sign‑in Logs retained ≥ 30 days (free tier 7 days + export).  
- Daily review of failed logins, foreign IPs, and legacy‑auth attempts.  
- Alert thresholds: ≥ 5 failed logins in 5 min, or any login from geo‑blocked region.

### 4.7  Incident Response
Follow the **Incident Response Flow** (`logs/incident-response.png`).  
Critical incidents (privileged account compromise) must be reported to CISO within **30 minutes**.

---

## 5  Compliance Mapping
| Control Family | Standard | Clause |
|----------------|----------|--------|
| Identification & Authentication | NIST 800‑53 IA‑2(1) | MFA for network access |
| Access Control | ISO 27001 A.9 | Least privilege |
| Security Monitoring | CIS Control 8 | Audit log management |

---

## 6  Exceptions & Deviations
Requests must be submitted to Security Team with business justification.  
Temporary exceptions limited to 30 days and logged in risk register.  
Permanent deviations require CISO approval.

---

## 7  Review & Maintenance
Policy reviewed annually or after major architecture changes.  
Security Team maintains version history in the `policies/` folder of the repository.

---

## 8  Acknowledgement
All employees, contractors, and third‑party users must read and sign this policy before receiving credentials.

---

_This document is part of a student lab demonstrating best‑practice governance in Azure Entra ID without premium licensing. 
