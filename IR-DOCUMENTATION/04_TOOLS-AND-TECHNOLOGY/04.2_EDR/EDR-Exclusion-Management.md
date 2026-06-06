# GUIDE: EDR Exclusion Management

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | GUIDE – EDR Exclusion Management |
| Document ID | TOOL-EDR-004 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / Endpoint Security Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This guide defines the governance, workflow, approval standards, and documentation requirements for managing EDR exclusions (also called allowlists, suppressions, detection exclusions, or policy exceptions) in order to:

- Reduce false positives and operational noise
- Prevent business disruption from legitimate software being blocked
- Maintain detection coverage and avoid blind spots
- Ensure exclusions are controlled, justified, time-bound, and auditable
- Support regulatory and audit requirements (ISO 27001/NIST/RBI expectations)

Improper exclusion practices can create major security gaps and are a common root cause of successful attacks, because exclusions can:

- Prevent detection of real threats (attacker uses excluded path/name)
- Disable telemetry visibility
- Reduce prevention effectiveness
- Allow malware to execute undetected
- Create cross-tenant risk in MSSP environments

This guide ensures:

- Strict approval workflows
- Evidence-based exclusion decisions
- Time-bound exclusions with expiry
- Centralized tracking and periodic review
- Tenant-safe exclusion application in MSSP environments
- Audit-ready change logs

---

# 3. Scope

This guide applies to exclusions for:

| Exclusion Type | Example |
|---|---|
| Process exclusion | Exclude `backup.exe` behavior |
| File hash exclusion | Allow specific signed binary |
| Path exclusion | Exclude `C:\Program Files\App\` |
| Certificate/signer exclusion | Allow trusted publisher |
| Detection rule suppression | Suppress specific detection rule |
| Sensor/agent exclusion | Limited telemetry changes (restricted) |
| Network exclusion (EDR) | Allow known management endpoints |
| Behavioral suppression | Known benign behavior pattern |

Out of scope:

- Firewall allow rules (handled under network change control)
- SIEM rule suppression (handled under SIEM tuning)
- IAM policy exceptions (handled under IAM governance)

---

# 4. Exclusion Management Philosophy (IMPORTANT)

Exclusions are **risk acceptance** decisions. They must be treated with the same governance rigor as security policy exceptions.

Core principles:

| Principle | Requirement |
|---|---|
| Least privilege | Exclude the minimum needed |
| Specificity | Prefer hash/signer over path |
| Time-bound | Always set an expiration |
| Evidence-based | Require telemetry and justification |
| Multi-approval | High-impact exclusions require higher approval |
| Continuous review | Monthly/quarterly review required |
| Tenant safety (MSSP) | Never apply cross-client exclusions |

Preferred exclusion order (from safest to riskiest):

1. **Hash exclusion (specific binary hash)**
2. **Signer/certificate exclusion (trusted publisher)**
3. **Process exclusion (specific process with command line constraints if possible)**
4. **Path exclusion (last resort; high risk)**

Avoid broad exclusions like:

- Entire drive exclusions (`C:\`)
- Entire user profile exclusions (`C:\Users\*`)
- Entire temp directories (`%TEMP%`)
- Wildcard process families (`*update*`)
- Disabling telemetry or tamper protection

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| Requestor (IT/App Owner) | Provide business justification and software details |
| L2 SOC Analyst | Validate false positive evidence and scope |
| Endpoint Security Lead | Implement and validate exclusions |
| Detection Engineering Lead | Assess detection impact; propose alternatives |
| SOC Manager | Approve medium/high risk exclusions |
| CISO | Approve critical/broad exclusions |
| Compliance/Risk | Review exception alignment and retention |
| MSSP Service Delivery | Client communication and approval tracking (MSSP) |

---

# 6. Exclusion Request Workflow

| Phase | Objective | Output |
|---|---|---|
| Phase 1 | Request intake | Ticket created with required fields |
| Phase 2 | Evidence validation | Confirm false positive and scope |
| Phase 3 | Risk assessment | Risk rating and recommendation |
| Phase 4 | Approval | Formal approval recorded |
| Phase 5 | Implementation | Exclusion applied in correct policy group |
| Phase 6 | Validation | Confirm reduced FP and no detection gap |
| Phase 7 | Documentation | Update exclusion register |
| Phase 8 | Review and expiry | Periodic review and removal |

---

# 7. Phase 1 — Request Intake (Mandatory Fields)

## 7.1 Exclusion Request Form (Table)

| Field | Required | Notes |
|---|---|---|
| Request ID / Ticket ID | Yes | Must be traceable |
| Requestor name/team | Yes | Business owner |
| Business justification | Yes | Why exclusion is needed |
| Application name/version | Yes | Include vendor |
| Environment | Yes | Prod/Non-prod |
| Hosts/Group scope | Yes | Limit scope |
| Exclusion type | Yes | hash/signer/path/process |
| Indicators | Yes | hash, path, command line |
| Evidence of false positive | Yes | EDR alert IDs, logs |
| Start date | Yes | |
| Expiry date | Yes | Mandatory |
| Compensating controls | Recommended | If broad exclusion |
| Approval required | Yes | Based on risk |

---

# 8. Phase 2 — Evidence Validation (SOC Requirements)

## 8.1 Evidence Validation Checklist

| Validation Item | Completed |
|---|---|
| Alert reviewed | ☐ |
| Behavior confirmed benign | ☐ |
| Vendor signature validated (if applicable) | ☐ |
| Hash verified (if applicable) | ☐ |
| Scope minimized | ☐ |
| Alternative tuning considered | ☐ |
| Risk rating assigned | ☐ |

## 8.2 Validation Evidence Types

| Evidence | Examples |
|---|---|
| EDR telemetry | Process tree, command line |
| File metadata | Signature, hash |
| Vendor documentation | Release notes |
| Change tickets | Planned deployment |
| IT confirmation | Admin request |
| Sandbox analysis (if required) | File behavior report |

---

# 9. Phase 3 — Risk Assessment

## 9.1 Risk Rating Matrix (Exclusions)

| Risk Level | Description | Typical Examples |
|---|---|---|
| Low | Highly specific exclusion | Single hash exclusion |
| Medium | Scoped process exclusion | Signed binary with fixed path |
| High | Path exclusion or broad process exclusion | Folder exclusion for app |
| Critical | Disabling telemetry/tamper protection or wide exclusions | Excluding Temp directories |

## 9.2 Risk Assessment Table

| Item | Assessment |
|---|---|
| Exclusion type risk | Low/Medium/High/Critical |
| Scope (hosts/groups) | Minimal / broad |
| Attack abuse potential | Low / medium / high |
| Data sensitivity of affected hosts | Low / medium / high |
| Alternatives available | Yes/No |
| Compensating controls required | Yes/No |
| Recommendation | Approve/Reject/Modify |

---

# 10. Phase 4 — Approval Requirements

## 10.1 Approval Matrix

| Exclusion Type | Risk | Minimum Approval |
|---|---|---|
| Hash exclusion | Low | Endpoint Security Lead |
| Signer/cert exclusion | Medium | SOC Manager |
| Process exclusion (scoped) | Medium | SOC Manager |
| Path exclusion | High | SOC Manager + Detection Eng Lead |
| Broad exclusions (multi-groups) | High | CISO |
| Telemetry reduction / tamper changes | Critical | CISO + Compliance |

## 10.2 Approval Record

| Field | Value |
|---|---|
| Approved By |  |
| Approval Date (UTC) |  |
| Approval Conditions |  |
| Expiry Date |  |
| Review Owner |  |

---

# 11. Phase 5 — Implementation Standards

## 11.1 Implementation Principles

| Principle | Requirement |
|---|---|
| Limit scope | Apply to minimum groups/hosts |
| Prefer safer exclusion types | hash/signer over path |
| Set expiry | Mandatory |
| Label clearly | Include ticket ID in description |
| Avoid cross-tenant impact | MSSP segregation |

## 11.2 Implementation Checklist

| Step | Completed |
|---|---|
| Correct policy/group identified | ☐ |
| Exclusion scope confirmed | ☐ |
| Expiry configured | ☐ |
| Ticket ID referenced in exclusion | ☐ |
| Change documented | ☐ |

---

# 12. Phase 6 — Validation After Implementation

## 12.1 Validation Objectives

| Objective | Purpose |
|---|---|
| Confirm false positives reduced | Operational effectiveness |
| Confirm no new blind spot | Security coverage |
| Confirm telemetry still intact | Investigation ability |
| Confirm no policy drift | Governance |

## 12.2 Validation Checklist

| Validation Item | Completed |
|---|---|
| Alert volume reduced | ☐ |
| No true positives suppressed | ☐ |
| Telemetry still available | ☐ |
| Detection coverage validated | ☐ |

---

# 13. Phase 7 — Exclusion Register (Mandatory)

All exclusions must be recorded in a register.

## 13.1 Exclusion Register Table

| Exclusion ID | Ticket ID | Client/Tenant | Type | Value (Hash/Path/etc.) | Scope | Risk | Owner | Start | Expiry | Status |
|---|---|---|---|---|---|---|---|---|---|---|
| | | | | | | | | | | |

---

# 14. Phase 8 — Review, Expiry and Removal

## 14.1 Review Frequency

| Risk Level | Review Frequency |
|---|---|
| Low | Quarterly |
| Medium | Monthly |
| High | Bi-weekly |
| Critical | Weekly |

## 14.2 Expiry Rules

| Rule | Requirement |
|---|---|
| Default expiry period | 30–90 days maximum (unless justified) |
| No expiry = not allowed | Mandatory fix |
| Renewal requires re-validation | Mandatory |
| Stale exclusions must be removed | Mandatory |

## 14.3 Expiry Review Table

| Exclusion ID | Expiry Date | Renewal Required? | Decision | Approved By |
|---|---|---|---|---|
| | | | | |

---

# 15. MSSP-Specific Controls (IMPORTANT)

For MSSP environments:

| Requirement | Purpose |
|---|---|
| Tenant-specific exclusions only | Prevent cross-client exposure |
| Client approval required for high-risk exclusions | Contract compliance |
| Client-specific registers | Audit readiness |
| Segregated implementation | Maintain data boundaries |
| Document in client profile | Traceability |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 16. Common Mistakes

| Mistake | Risk |
|---|---|
| Broad path exclusions | Malware abuse potential |
| No expiry date | Permanent blind spot |
| No evidence validation | Wrong exclusion |
| No approval record | Governance failure |
| Applying to too many hosts | Increased risk |
| Cross-tenant exclusion | MSSP compliance breach |

---

# 17. Related Documents

| Document | Path |
|---|---|
| EDR Alert Handling Guide | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Alert-Handling-Guide.md` |
| EDR Investigation Queries | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Investigation-Queries.md` |
| EDR Deployment Coverage Check | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Deployment-Coverage-Check.md` |
| SIEM Alert Tuning Guide | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md` |
| Policy Exception Register | `00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md` |
| Client Data Segregation Policy | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md` |

---

# 18. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | Endpoint Security Lead | Initial version |

---

# 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**