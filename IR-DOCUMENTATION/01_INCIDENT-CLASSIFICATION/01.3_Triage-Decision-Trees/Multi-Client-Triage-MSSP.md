# Multi-Client Triage (MSSP) – Standard Decision Tree and Handling Rules

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Multi-Client Triage (MSSP) |
| Document ID | IR-TRIAGE-004 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | MSSP SOC Manager / Service Delivery Manager |
| Approved By | CISO / MSSP Delivery Head |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Purpose

This document defines the standard triage and incident handling rules for
MSSP environments where multiple client tenants are monitored and
supported by a shared SOC.

It ensures:
- correct client attribution for every alert and incident
- strict client data segregation and confidentiality
- consistent severity classification with client-specific requirements
- SLA-compliant escalation and communications for each client
- controlled evidence handling and secure sharing
- prevention of cross-client contamination in tickets and reporting

---

## 3. Scope

Applies to:
- all alerts and incidents handled in MSSP context
- multi-tenant SIEM deployments
- centralized EDR consoles supporting multiple clients
- client ticketing portals or shared ticketing systems
- all SOC tiers (L1/L2/L3), SOC Leads, and IR Team

Includes:
- alert triage and qualification
- incident severity classification
- escalation and notification
- evidence handling and client sharing
- cross-client incident scenarios

---

## 4. Core Principles (Non-Negotiable)

1. Client data segregation must be maintained at all times.
2. No cross-client evidence sharing, referencing, or leakage is permitted.
3. Every alert must be mapped to the correct client and environment scope.
4. Client SLAs and notification timelines override internal defaults where contracted.
5. All high-impact containment actions require client approval unless pre-approved.
6. Use the ticket as the single source of truth for each client incident.
7. Maintain audit-ready evidence trails for each client separately.

---

## 5. Roles and Responsibilities (MSSP Context)

| Role | Responsibilities |
|------|------------------|
| MSSP L1 Analyst | Initial triage, correct client mapping, ticket creation, basic enrichment |
| MSSP L2 Analyst | Deep investigation, incident confirmation, scope definition, containment recommendation |
| MSSP L3 Analyst | Advanced analysis, threat hunting, forensic guidance, cross-client correlation (without data leakage) |
| SOC Lead | Incident coordination, severity approvals, SLA governance, client notification enforcement |
| Service Delivery Manager (SDM) | Client communication governance, SLA reporting, escalation to account leadership |
| IR Team | Major incidents, forensic collection, coordinated containment and recovery support |
| Client Security Owner | Approves high-impact containment, owns regulatory decisions, confirms closure |
| Client IT/Network/IAM | Executes containment actions in client environment (unless delegated) |

Reference:
- `00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md`
- `00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`

---

## 6. Multi-Client Triage Workflow (Standard)

### Step 1: Client Attribution (Mandatory First Step)

For every alert, confirm:

- client name and tenant identifier
- environment name (prod/non-prod)
- log source ownership (client-owned vs MSSP-shared)
- asset ownership (client asset vs MSSP infrastructure)
- whether the alert is scoped to a single client or shared platform

Do not proceed with any action until attribution is confirmed.

Required ticket fields:
- Client Name
- Client Tenant ID
- Client Environment
- Asset Owner
- Contact Group (Client escalation group)

---

### Step 2: Validate Data Segregation Requirements

Before opening logs, attachments, or sharing evidence:

- confirm the ticket is in the correct client queue
- confirm the analyst has access rights for the client
- confirm artifacts will be stored only in client-approved locations
- confirm that screenshots do not include other tenants

If any risk of cross-tenant exposure exists, stop and escalate to SOC Lead.

---

### Step 3: Initial Triage and Enrichment (Client-Specific)

Enrich using client-specific sources where contracted:

- SIEM (client tenant)
- EDR telemetry (client group)
- firewall/proxy logs (client)
- identity logs (client IAM)
- cloud audit logs (client)
- threat intelligence enrichment (global allowed, but outputs must be scoped per client)

Document enrichment sources clearly.

---

### Step 4: Qualification and Severity Assignment

Use standard qualification rules:

Reference: `01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/Alert-to-Incident-Qualification.md`

However, apply client severity adjustments if the client contract defines them.

Client-specific severity policies are stored under:
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/`

If client severity differs, record:
- MSSP default severity
- Client severity
- final ticket severity (client priority governs client comms/SLA)

---

### Step 5: SLA and Notification Triggers

For each client incident, apply:

- contracted SLA timers
- client notification timelines
- client escalation contact rules
- after-hours contact requirements

Reference:
- `00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`
- `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md`

---

### Step 6: Escalation and Containment Approval Rules

Containment actions must follow the client responsibility matrix.

High-impact actions typically require client approval:

- endpoint isolation
- disabling user accounts
- firewall blocks that may impact business
- network segmentation
- service shutdowns

Pre-approved actions must be documented per client.

Reference:
- `00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md`

---

## 7. Client Data Segregation Rules

### 7.1 Ticketing Rules
- never include another client’s name in ticket notes
- never attach screenshots containing other client data
- never paste indicators that include other tenants’ proprietary information
- use only the client’s ticket queue and client tags

### 7.2 Evidence Storage Rules
- store evidence in client-specific storage location only
- use client-specific naming standards (incident ID + client ID)
- ensure encryption at rest and in transit as per contract

### 7.3 Reporting Rules
- client reports must contain only that client’s data
- cross-client trend reporting must be anonymized and aggregated
- any sharing of threat intelligence outputs must be de-identified unless explicitly permitted

---

## 8. Cross-Client Correlation Without Data Leakage

Cross-client analysis may be required to identify widespread campaigns.
This must be done without leaking details.

Allowed correlation outputs:
- generic IOC lists (domain/IP/hash) without client attribution
- generic TTP patterns (MITRE techniques) without client evidence
- campaign-level summaries without names, counts, or proprietary details

Not allowed:
- sharing client log samples across clients
- revealing affected client identities
- sharing incident timelines of one client with another
- sharing client-specific vulnerabilities or exposure details

If a widespread campaign is suspected:
- SOC Lead and SDM must be notified
- incident handled as separate tickets per client
- shared threat intel bulletin can be created if allowed

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`

---

## 9. Multi-Client Triage Decision Rules (Priority and Queue)

When multiple clients generate alerts simultaneously:

Priority order should consider:

1. P1 incidents for any client
2. P2 incidents with potential for escalation
3. P1/P2 incidents for regulated clients (if SLA requires)
4. P3 incidents with suspicious patterns
5. P4 informational events

SOC Lead may re-allocate analysts to meet SLA and prevent P1 delays.

---

## 10. Multi-Client Bridge Call Rules (P1/P2)

Bridge calls must be client-separated unless explicitly approved.

Rules:
- one bridge call per client incident
- only invite client-approved participants
- avoid discussing other client incidents
- keep minutes and actions documented in client ticket

If MSSP infrastructure is impacted:
- bridge call may include internal MSSP leadership only
- client bridge calls must be separate per impacted client

Reference:
`03_SOC-TIER-PROCEDURES/03.4_SOC-Lead-Procedures/SOCLead-P1-P2-Bridge-Call-SOP.md`

---

## 11. MSSP Escalation and Communication Requirements

### 11.1 Minimum Client Notification Contents
Client notifications must include:

- incident ID and severity
- affected assets (as known)
- what was detected and when
- actions taken by MSSP
- actions required from client
- recommended containment steps
- next update time

Use standard templates:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md`

### 11.2 Communication Approval
- P1/P2 client updates must be approved by SOC Lead or SDM
- regulatory communications must be approved by client owner and legal/compliance

---

## 12. MSSP Evidence Handling and Chain-of-Custody

For incidents requiring forensic evidence:

- evidence must be logged under client incident ID
- chain-of-custody forms must reference client and case ID
- evidence transfer to client must be encrypted and documented
- evidence retention must follow client contract and legal requirements

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 13. Common MSSP Triage Mistakes to Avoid

| Mistake | Impact | Prevention |
|--------|--------|------------|
| Wrong client attribution | SLA breach, data exposure | confirm tenant before triage |
| Copy/paste from other client ticket | confidentiality breach | enforce ticketing discipline |
| Broad whitelisting | reduces detection effectiveness | scope allowlists per client only |
| Overlooking client-specific SLAs | missed notification deadlines | maintain client SLA matrix |
| Combining clients into one bridge call | confidentiality breach | separate calls and documentation |
| Sharing exposure details across clients | contractual breach | use anonymized intelligence bulletins only |

---

## 14. Related Documents

| Document | Path |
|---------|------|
| Master Triage Decision Tree | `01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/Master-Triage-Decision-Tree.md` |
| Alert-to-Incident Qualification | `01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/Alert-to-Incident-Qualification.md` |
| False Positive Handling | `01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/False-Positive-Handling.md` |
| MSSP Client SLA Template | `00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md` |
| MSSP Responsibility Matrix | `00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md` |
| Client Customization | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/` |
| Cross-Client Incident Procedure | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md` |

---

## 15. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | MSSP SOC Manager | Initial version |

---

## 16. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

End of Document