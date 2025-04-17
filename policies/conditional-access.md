# Conditional Access Strategy (Design‑Only)

> **File:** `policies/conditional-access.md`  
> _(Implementation requires Azure AD Premium P1; the free tier lets us plan and document these policies without enforcing them.)_

---

## 1  Why Conditional Access?

**Zero‑Trust Principle** → Never assume trust, always verify context  
**Unified Risk Engine** → Uses sign‑in risk, device health & location signals  
**Granular Controls** → Enforce MFA, block, or limit sessions dynamically

Because the free tier doesn’t apply CA rules, we treat this as an architecture & policy design exercise, a standard expectation in portfolios.

---

## 2  Policy Catalogue

| # | Policy Name | Users / Groups | Conditions | Access Controls | Business Goal |
|---|-------------|---------------|------------|-----------------|---------------|
| **P‑01** | _Block Outside Canada & USA_ | **All Users** | Location ≠ CA/USA | **Block** | Mitigate global password‑spray & geo‑spoof attacks |
| **P‑02** | _Risky Sign‑In Password Reset_ | All Users | Sign‑in risk **≥ Medium** | **Require Password Change** | Contain credential theft; force user verification |
| **P‑03** | _Intern Work‑Hours Access_ | `Interns` Security Group | Time outside 09:00‑18:00 EST | **Block** | Reduce after‑hours misuse of low‑privilege accounts |
| **P‑04** | _Guest MFA Enforcement_ | `Guests`, `vendor@ext.com` | — | **Require MFA** | Protect supply‑chain entry points |
| **Baseline** | _MFA for All Users_ | All Users (per‑user MFA) | — | **Require MFA** | Free‑tier enforcement; foundation for all other rules |

---

## 3  Named Locations & Time‑Based Targets

### Trusted Locations  
- **Canada** (Country)  
- **United States** (Country)

### Work Hours (Eastern Time)  
`09:00` → `18:00` Monday–Friday

> *Azure CA time controls are Premium; schedule expressed here for documentation & future deployment.*

---

## 4  Implementation Playbook (Premium P1)

### Example: _Block Outside Canada & USA_

1. **Security → Conditional Access → + New Policy**  
2. **Assignments**  
   - _Users_: **All users**  
   - _Locations_: Include **Any Location** → Exclude **Canada**, **United States**  
3. **Access Controls** → **Block Access**  
4. **Enable Policy** → _On_  

_Repeat analogous steps for other policies, swapping Conditions & Controls._

---

## 5  Free‑Tier Simulation Steps

1. **Document** policies (this file).  
2. **Create Named Locations** (allowed in free tier).  
3. **Generate Evidence**: screenshots of location objects & policy draft UI (not enforced).  
4. **Reference Logs**: Note that sign‑in logs would show denials once premium is enabled.

---

## 6  Monitoring & Alerting Plan

| Policy | Log Signal | SOC Action |
|--------|-----------|------------|
| P‑01 | Sign‑in failures from geo‑blocked IPs | Validate IP, open incident if repeated |
| P‑02 | `PasswordChangeRequired` events | Ensure user completes reset; check for malicious IP |
| P‑03 | After‑hours sign‑in attempts by `Interns` | Temporary disable + manager notification |
| P‑04 | Guest login without MFA challenge | Investigate device compliance & guest lifecycle |

For full production, integrate Microsoft Sentinel or Defender for Cloud Apps to alert on CA policy matches.

---

## 7  Future Enhancements

| Iteration | Feature | Benefit |
|-----------|---------|---------|
| v2 | Sign‑in Risk Policies (Identity Protection) | Automate response to impossible travel & TOR exit nodes |
| v3 | Device Compliant Access | Combine Intune posture with user context |
| v4 | Continuous Access Evaluation (CAE) | Real‑time session revocation on token risk changes |

---

> Documenting robust CA policies now means faster deployment when premium features become available.
