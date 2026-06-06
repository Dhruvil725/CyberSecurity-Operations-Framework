# MSSP – Client Responsibility Matrix (Incident Response)

---

## 1. Document Control

| Field | Value |
|-------|--------|
| Document Name | MSSP–Client Responsibility Matrix (IR) |
| Document ID | IR-GOV-001 |
| Version | 1.0 |
| Effective Date | 14-May-2026 |
| Owner | MSSP SOC Manager / Service Delivery Manager |
| Approved By | CISO / Contract Owner |
| Classification | Confidential |
| Review Cycle | Quarterly / Contract Change |

---

## 2. Purpose

This document defines the division of responsibilities between the MSSP and the Client for incident response activities, including monitoring, triage, investigation, containment, eradication, recovery, communications, and regulatory reporting.

It is intended to:
- Prevent gaps or duplication during incidents
- Define decision authority and approval points
- Support ISO 27001 / NIST / RBI audit expectations
- Align operational activities with contractual SLAs

---

## 3. Scope

Applies to all security incidents affecting:
- Client environments monitored by MSSP (SIEM/EDR/network/cloud)
- MSSP-managed security platforms and workflows
- Joint response actions requiring client approval

Out of scope unless contracted:
- Full digital forensics and incident reconstruction
- On-site IR support
- Legal representation and regulatory filing (client-owned)
- Business continuity / disaster recovery execution (client-owned)

---

## 4. Definitions (RACI)

- **R (Responsible):** Performs the activity
- **A (Accountable):** Owns final outcome/decision (approver)
- **C (Consulted):** Provides input
- **I (Informed):** Must be notified/updated

---

## 5. Parties & Roles

### 5.1 MSSP Roles (typical)
- MSSP L1 SOC Analyst
- MSSP L2 SOC Analyst
- MSSP L3 / Threat Specialist
- MSSP SOC Lead / Incident Coordinator
- MSSP IR Team (if included in contract)
- MSSP Service Delivery Manager (SDM)

### 5.2 Client Roles (typical)
- Client Security / CISO / ISO
- Client IT Operations
- Client Network Team
- Client IAM / AD Team
- Client Application Owner
- Client GRC / Compliance
- Client Legal
- Client PR / Communications (if needed)

---

## 6. Responsibility Matrix (RACI)

> Customize this table per client contract. Add/remove rows based on scope.

| Activity | MSSP | Client | Notes / Approval Points |
|---------|------|--------|--------------------------|
| Define IR policy & governance | C | A/R | Client owns policy; MSSP provides guidance |
| Maintain monitoring coverage (SIEM/EDR) | R | C | Based on agreed log sources and coverage |
| Alert triage (initial) | R | I | L1/L2 triage; client informed for defined severities |
| Incident declaration (P1/P2) | R | A | MSSP recommends/declares per runbook; client accountable for business impact classification |
| Severity classification | R | A | MSSP proposes; client confirms business criticality impact |
| Evidence collection (logs, EDR telemetry) | R | C | MSSP collects available telemetry within tooling access |
| Evidence preservation & retention | R | A | Client accountable for retention obligations; MSSP follows CoC for artifacts handled |
| Endpoint isolation (EDR network containment) | R (with approval) | A | Requires client approval unless “pre-approved actions” defined |
| Firewall block / perimeter changes | C | A/R | Client executes changes unless MSSP has delegated authority |
| Disable user accounts / reset credentials | C | A/R | Client IAM executes; MSSP can recommend scope |
| Malware removal / host remediation | C | A/R | Client IT executes remediation actions |
| Patch / configuration remediation | C | A/R | Client owns change mgmt + patching |
| Threat hunting during incident | R | C | Per contract; outputs shared with client |
| Regulatory reporting (RBI/CERT-In/etc.) | I/C | A/R | Client is accountable and files reports; MSSP provides technical inputs |
| Client executive updates | R (technical) | A/R | Client owns executive/business communications |
| External communications (customers/media) | I | A/R | Client only (Legal/PR) |
| Recovery / restore from backups | I/C | A/R | Client owns BCP/DR and restore execution |
| Return-to-service decision | I/C | A/R | Client business owner approves; MSSP provides risk assessment |
| Post Incident Review (PIR) | R/C | A/R | Joint PIR recommended; client owns action closure |
| Corrective action tracking | C | A/R | Client owns implementation; MSSP supports detection improvements |
| Close incident ticket | R | A | Closure requires client confirmation for P1/P2 |

---

## 7. Pre-Approved Actions (Optional – Strongly Recommended)

To speed response, the client may pre-approve the following actions for MSSP (tick what applies):

| Action | Pre-Approved? (Yes/No) | Conditions / Limits |
|-------|--------------------------|---------------------|
| Isolate end-user endpoints via EDR |  | Only non-critical endpoints |
| Block known malicious hashes in EDR |  | Based on TI confidence threshold |
| Block IoC domains in DNS/Proxy (if integrated) |  | Must not impact business domains |
| Quarantine phishing emails (if integrated) |  | Must retain copy for evidence |
| Disable compromised user accounts |  | Only after client approval unless emergency clause |
| Collect triage artifacts (process list, autoruns, etc.) |  | Must follow evidence SOP |

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

## 8. Notification & Escalation Responsibilities

### 8.1 MSSP Notification Responsibilities
MSSP must notify the client when:
- P1 / P2 incident declared
- Confirmed compromise of privileged accounts
- Confirmed malware execution/ransomware behavior
- Suspected/confirmed data exfiltration
- Material service disruption linked to security

### 8.2 Client Notification Responsibilities
Client must:
- Provide 24x7 escalation contacts
- Join bridge calls for P1/P2 within agreed SLA
- Approve high-impact containment actions promptly
- Inform MSSP about business criticality and operational constraints

Reference:
`05_ESCALATION-AND-COMMUNICATION/`

---

## 9. Tooling, Access, and Limitations

| Area | MSSP Responsibility | Client Responsibility |
|------|---------------------|----------------------|
| SIEM access | Operate and monitor | Provide log sources and maintain integrations |
| EDR access | Investigate and respond within permissions | Maintain endpoint coverage and agent health |
| Ticketing | Create/maintain tickets | Provide ticket workflow/approvals if client-owned |
| Network controls | Recommend blocks | Implement blocks unless delegated |
| Admin access | Limited to contracted scope | Provide break-glass access if required (controlled) |

---

## 10. Data Ownership & Confidentiality

- Client retains ownership of all client logs, telemetry, and evidence.
- MSSP must maintain confidentiality and tenant segregation.
- Evidence shared externally requires client approval (Legal/Compliance).

---

## 11. Exceptions

Any deviations from this matrix must be documented in:
`00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md`

---

## 12. Client-Specific Customization Block

| Client Name |  |
|-------------|--|
| Contract/SOW Reference |  |
| SLA Reference |  |
| Primary Contacts |  |
| Notification Windows |  |
| Pre-approved Actions |  |
| Special Constraints (e.g., no isolation during business hours) |  |

---

## 13. Approval

**MSSP Approval**  
Name: ____________________  
Title: ____________________  
Date: ____________________

**Client Approval**  
Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**