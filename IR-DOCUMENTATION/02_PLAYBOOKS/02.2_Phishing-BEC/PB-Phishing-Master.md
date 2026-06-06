# Playbook: Phishing and BEC (Master)

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Phishing and BEC (Master) |
| Document ID | IR-PB-PHB-001 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | SOC Manager / IR Team Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 phishing or BEC incident |

---

## 2. Purpose

This master playbook defines the end-to-end response procedure for:

- phishing (credential phishing, malware phishing, social engineering)
- business email compromise (BEC), including impersonation and account takeover
- OAuth consent abuse and cloud identity-driven phishing outcomes

It standardizes:
- alert qualification and severity assignment
- investigation and scoping across email, identity, endpoint, and network logs
- containment actions (mailbox, identity, endpoint, and perimeter controls)
- eradication actions (rule removal, token revocation, credential resets, IOC blocking)
- evidence handling and reporting requirements
- MSSP client notification and segregation requirements

---

## 3. Scope

Applies to:
- enterprise internal email and identity platforms
- MSSP-managed client email and identity platforms (per contract)
- user-reported suspicious emails
- SIEM alerts from email gateway, proxy, IAM, and EDR
- BEC-related financial fraud attempts or confirmations
- follow-on compromises originating from phishing (endpoint malware, token theft, mailbox takeover)

Out of scope unless explicitly contracted or approved:
- public communications (owned by Legal/PR)
- insurance claim handling
- law enforcement engagement (owned by Legal/Management)
- funds recovery actions with banks (owned by Finance/Legal; SOC supports evidence)

---

## 4. Definitions

| Term | Definition |
|------|------------|
| Phishing | Deceptive message intended to steal credentials or deliver malware |
| BEC | Impersonation or takeover of business email to commit fraud or steal information |
| Mailbox Takeover | Unauthorized access to email account, often used for forwarding/rules and internal phishing |
| OAuth Consent Abuse | User grants permissions to a malicious application, enabling access without password reuse |
| AiTM | Adversary-in-the-middle phishing that can intercept MFA tokens/sessions |
| Phishing Campaign | Same lure delivered to multiple recipients |
| Disposition | Final classification outcome (Incident / BTP / FP / Informational / Duplicate) |

---

## 5. Severity Guidance (Phishing and BEC)

Severity is based primarily on user interaction, compromise confirmation, and business impact.

| Scenario | Default Severity |
|----------|------------------|
| Confirmed financial fraud / funds transferred | P1 |
| Mass mailbox compromise or widespread credential compromise | P1 |
| Confirmed mailbox takeover of privileged user (executive/finance/admin) | P1 or P2 (based on scope and impact) |
| Credentials entered on phishing page (confirmed) | P2 |
| Confirmed malicious OAuth grant / token abuse | P2 |
| Malware executed from phishing attachment | P2 (upgrade to P1 if lateral movement or critical systems affected) |
| User clicked link (no credential entry confirmed) | P3 |
| Email delivered, no interaction confirmed | P4 |
| Email blocked by gateway (no user interaction) | P4 |

References:
- `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`
- `01_INCIDENT-CLASSIFICATION/01.2_Incident-Categories/CAT-02-Phishing-BEC.md`

---

## 6. Activation Criteria (When to Use This Playbook)

Trigger this playbook when any of the following are detected or reported:

- user reports a suspicious email (attachment/link/login request)
- secure email gateway flags or quarantines suspected phishing
- SIEM alert indicates user clicked a suspicious URL
- identity platform indicates suspicious sign-in tied to email credential theft (impossible travel, risky sign-in)
- mailbox audit logs show suspicious rule creation, forwarding, delegate assignment, or OAuth grant
- outbound spam/phishing is sent from internal mailbox (possible takeover)
- finance team reports suspicious payment request or invoice change (possible BEC)

---

## 7. Roles and Responsibilities (Operational)

| Role | Responsibilities |
|------|------------------|
| L1 SOC Analyst | Validate alert/report, preserve original email evidence, basic enrichment, severity recommendation, escalate to L2/SOC Lead |
| L2 SOC Analyst | Confirm interaction and compromise, scope campaign, recommend containment, coordinate mailbox and identity response |
| L3 Analyst / Threat Specialist | Advanced correlation, threat intel integration, hunting, AiTM/OAuth investigations, complex compromise analysis |
| SOC Lead | Owns severity approval for P1/P2, coordinates response and communications, ensures SLA adherence |
| IR Team | Engages for P1, major BEC fraud, mass compromise, or cross-domain compromise (endpoint + identity + data) |
| Email Admin Team | Mail trace, purge, quarantine, allow/block lists, tenant-level security settings |
| IAM/Identity Team | Credential resets, session revocation, MFA policy enforcement, conditional access changes |
| IT Ops / Endpoint Team | Endpoint isolation, malware removal, device compliance actions |
| Finance / Procurement | Validate transactions, vendor banking changes, payment controls |
| GRC / Compliance | Regulatory assessment, reporting coordination, audit evidence |
| Legal | Legal guidance, evidence preservation, disclosure, law enforcement coordination |
| MSSP SDM (if applicable) | Client communications governance and SLA management |

Reference:
- `00_GOVERNANCE/00.3_Roles-and-Responsibilities/RACI-Matrix-IR.xlsx`
- `00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md`

---

## 8. Required Inputs (Minimum Data to Collect)

### 8.1 Email Evidence (Mandatory)
- original email preserved in a safe format (EML/MSG) where possible
- full headers (Received lines, Message-ID, Return-Path, Reply-To)
- sender address and display name
- subject, timestamps, recipient list
- URLs and domains present in body (including rewritten URLs by gateway)
- attachment names and hashes (if available)
- any sandbox or detonation result (if available)

### 8.2 User Interaction Evidence (Mandatory)
- open/click telemetry (gateway or user confirmation)
- confirmation of credential entry (user statement or log evidence)
- MFA prompt history (user-reported or identity logs)
- endpoint downloads/execution evidence (if applicable)

### 8.3 Identity Evidence (As Applicable)
- sign-in logs (location, device, client app, conditional access results)
- session/token activity (revocations, refresh token use)
- MFA enrollment changes
- password reset events

### 8.4 Mailbox Evidence (As Applicable)
- mailbox audit logs for:
  - forwarding rules
  - inbox rules
  - delegate permissions
  - mailbox access from unusual location/device
  - mass mail sent events

### 8.5 Business Context (BEC)
- impacted vendor/customer name (if known)
- invoice/payment request details
- whether funds were transferred (yes/no)
- whether payment instructions were changed
- timing constraints for recovery actions

---

## 9. Workflow Overview (End-to-End)

This playbook follows phases that may occur in parallel.

### Phase A: Triage and Qualification (L1/L2)
- validate email authenticity and indicators
- determine user interaction and severity
- open ticket and apply category CAT-02
- initiate campaign scoping

### Phase B: Containment
- remove/purge email from mailboxes (if campaign)
- block sender/domain/URL/hashes across controls
- if credential compromise suspected:
  - reset password and revoke sessions
  - enforce MFA and remove unknown MFA devices
- if malware suspected:
  - isolate endpoint and coordinate investigation

### Phase C: Investigation and Scoping
- identify all recipients and affected users
- determine if any accounts were compromised
- identify mailbox rules or OAuth grants indicating persistence
- determine whether attacker used mailbox to send additional phishing
- assess for BEC impact (fraud attempt/success)

### Phase D: Eradication
- remove malicious inbox rules and external forwarding
- remove malicious OAuth grants/app consents
- rotate credentials and invalidate tokens
- tune controls and detections to prevent recurrence

### Phase E: Post-Incident
- produce final incident report and executive summary (P1/P2)
- lessons learned and improvements tracked
- update detections and playbooks as required

---

## 10. Containment Actions (Decision Guidance)

### 10.1 Email Containment (Campaign-Level)
- quarantine or block sender and domains
- block URLs at email gateway and proxy
- purge email from all mailboxes (administrator action)
- update secure email gateway policies if detection gap identified

### 10.2 Identity Containment (Credential/Token Risk)
- reset password for impacted account
- revoke sessions and refresh tokens (cloud identity and email platform)
- remove unknown MFA devices and re-register MFA
- enforce conditional access restrictions temporarily (geo/device/app restrictions)
- for privileged users: apply accelerated privileged access lockdown

### 10.3 Mailbox Containment (Takeover Indicators)
- disable external auto-forwarding
- remove suspicious inbox rules
- remove delegate access not authorized
- review and disable suspicious mail app permissions
- restrict mailbox access temporarily if required (approval based)

### 10.4 Endpoint Containment (Malware Phishing)
- isolate endpoint via EDR if execution suspected
- collect EDR telemetry and artifacts
- block hashes and related IOCs

Reference:
- `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Containment.md`

---

## 11. Eradication Actions (Decision Guidance)

Eradication confirms removal of attacker persistence and reduces re-entry risk.

Common eradication items:
- remove forwarding and inbox rules created by attacker
- remove malicious OAuth consent grants and app registrations
- remove malicious mail connectors or transport rules (if abused)
- rotate compromised credentials and secrets
- confirm tokens invalidated and sessions revoked
- confirm endpoint is clean or rebuilt if malware executed

Reference:
- `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Eradication.md`

---

## 12. BEC-Specific Handling Requirements

### 12.1 Immediate Finance Coordination Triggers
Engage Finance and SOC Lead immediately if:
- payment request or bank detail change is reported
- invoice template appears altered or vendor communications are suspicious
- an executive impersonation is involved (CEO/CFO/Finance head)
- any transfer is pending or completed

### 12.2 Evidence Requirements for BEC Fraud
- original email chain and headers
- sender impersonation evidence (domain similarity, reply-to mismatch)
- mailbox audit logs if internal account suspected compromised
- timeline of communications and approvals
- payment instruction change details and timestamps
- confirmation of funds transferred or prevented

### 12.3 Severity Notes
- confirmed funds transfer: P1
- attempted fraud with strong indicators but no funds transferred: typically P2 (upgrade based on scale and role)

Reference:
- `02_PLAYBOOKS/02.2_Phishing-BEC/PB-BEC-Detection-Analysis.md`

---

## 13. Evidence Handling (Minimum Standard)

### 13.1 Evidence to Preserve for All Phishing Incidents
- email sample (EML/MSG), headers, URLs, attachment details
- list of recipients and delivery status
- user interaction evidence (click/open)
- disposition rationale (FP/BTP/Incident)

### 13.2 Additional Evidence for P2/P1 Incidents
- identity sign-in logs and MFA activity
- mailbox audit logs and rule exports
- endpoint telemetry (if malware)
- communications record (internal/client updates)
- chain-of-custody if evidence may be used legally or regulatorily

Reference:
- `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 14. Communication Requirements

### 14.1 Internal
- P2 and above: notify SOC Lead immediately
- P1/P2: management notification timelines per SLA and severity
- status updates at defined cadence (P1: 30 minutes; P2: 60 minutes)

### 14.2 MSSP Clients (If Applicable)
- notify client per SLA and contract
- do not share cross-client evidence
- record client approvals for containment actions

References:
- `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`
- `00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`

---

## 15. Quality Gates (Closure Criteria)

A phishing/BEC incident may be closed when:
- all malicious emails are removed or confirmed contained
- all impacted users are identified and remediated
- any compromised accounts have had:
  - password reset completed
  - sessions revoked
  - MFA integrity verified
- mailbox persistence mechanisms are removed (rules/forwarding/delegates/OAuth)
- monitoring shows no continued suspicious sign-ins or mail activity
- final report delivered for P1/P2 and PIR actions recorded

---

## 16. Playbook Links (Phishing and BEC Set)

| Document | Path |
|---------|------|
| Phishing Master | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Master.md` |
| L1 Triage | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L1-Triage.md` |
| L2 Investigation | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L2-Investigation.md` |
| L3 Forensics | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-L3-Forensics.md` |
| Containment | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Containment.md` |
| Eradication | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Eradication.md` |
| BEC Detection Analysis | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-BEC-Detection-Analysis.md` |
| MITRE Mapping | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-MITRE-Mapping.md` |

---

## 17. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | SOC Manager / IR Team Lead | Initial version |

---

## 18. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

End of Document