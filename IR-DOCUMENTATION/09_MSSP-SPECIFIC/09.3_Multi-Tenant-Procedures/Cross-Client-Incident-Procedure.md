# Cross-Client Incident Procedure (MSSP Multi-Tenant)

---

# 1. Document Control

| Field          | Value                                                    |
| -------------- | -------------------------------------------------------- |
| Document Name  | Procedure – Cross-Client Incident Handling               |
| Document ID    | MSSP-MT-002                                              |
| Version        | 1.0                                                      |
| Effective Date | 30-May-2026                                              |
| Owner          | MSSP SOC Manager / IR Team Lead                          |
| Approved By    | MSSP CISO                                                |
| Classification | Confidential – MSSP Internal                             |
| Review Cycle   | Annually (or upon multi-client incident lessons learned) |

---

# 2. Purpose

This document defines the standardized **Cross-Client Incident Procedure** governing how the MSSP detects, investigates, contains, and communicates during incidents that affect or potentially affect multiple clients simultaneously — while strictly preserving tenant segregation.

A formal cross-client incident procedure is critical because:

- single threat actors, campaigns, or vulnerabilities frequently affect multiple MSSP clients in parallel
- timely cross-client correlation enables proactive defense across the entire client portfolio
- inconsistent handling of multi-client incidents leads to disparate response and SLA breaches
- NIST CSF Detect (DE.AE) and Respond (RS.CO, RS.AN) functions require correlated detection and coordinated response
- ISO 27001 Annex A.5.7 and A.5.24 require threat intelligence and structured response
- RBI Cyber Security Framework expects coordinated, threat-informed defense
- without strict procedure, cross-client correlation can lead to data segregation breaches
- multi-tenant incidents often involve regulated entities with different reporting timelines
- threat intelligence sharing (sanitized) must be balanced with client confidentiality
- common vulnerabilities (zero-day, supply chain) require rapid portfolio-wide assessment
- coordinated containment may have efficiency benefits but requires careful authorization
- communication to multiple clients about the same threat requires consistent messaging
- regulatory reporting (CERT-In, RBI) requires per-client attribution and timelines
- post-incident learnings must be applied across the portfolio with sanitization
- audit and compliance reviews require evidence of structured multi-client handling
- this procedure operationalizes the Client Data Segregation Policy in incident scenarios

This procedure ensures:

- structured detection and correlation of multi-client threats
- defined roles for cross-client incident commander, analysts, and SDMs
- mandatory tenant segregation throughout investigation and response
- per-client incident handling with portfolio-level coordination
- sanitized cross-client intelligence sharing
- consistent communication aligned per client
- coordinated regulatory reporting where applicable
- linkage to TI, detection engineering, playbook updates, and lessons learned
- audit-ready evidence of structured multi-client response

Reference alignment:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`
`08_POST-INCIDENT/08.4_Threat-Intel-Output/TTP-Intelligence-Report.md`
`02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-Master.md`

---

# 3. Scope

This procedure applies to incidents/threats affecting multiple MSSP clients:

| Cross-Client Scenario                          | Examples                                                        |
| ---------------------------------------------- | --------------------------------------------------------------- |
| **Common Vulnerability Exploitation**          | Zero-day affecting Log4j, MOVEit, Exchange                      |
| **Common Threat Actor Campaign**               | APT or cybercriminal targeting industry/region                  |
| **Supply Chain Attack**                        | Compromise of common vendor (SolarWinds-class)                  |
| **Common Phishing Campaign**                   | Mass phishing targeting multiple clients                        |
| **Ransomware Campaign**                        | Same ransomware family across clients                           |
| **Industry-Specific Attack Wave**              | BFSI-targeted credential stuffing                               |
| **Geographic Attack Wave**                     | Region-specific DDoS campaign                                   |
| **Common Cloud Misconfiguration Exploitation** | AWS/Azure/GCP-targeted attacks                                  |
| **Common SaaS Provider Incident**              | M365 / Salesforce / Okta compromise                             |
| **Common IoC Detection**                       | Same IoCs detected across multiple clients                      |
| **Common Insider Pattern**                     | Same behavioral pattern across clients (rare; high sensitivity) |

Out of scope:

- Single-client incidents (covered by standard playbooks)
- Coincidental but unrelated incidents
- Generic threat intelligence advisories without active exploitation
- MSSP-internal incidents not affecting clients

---

# 4. Definitions

| Term                                   | Definition                                                                |
| -------------------------------------- | ------------------------------------------------------------------------- |
| Cross-Client Incident                  | Incident affecting two or more MSSP clients with common root cause/threat |
| Portfolio Impact                       | Number and criticality of clients affected                                |
| Cross-Client Incident Commander (CCIC) | Designated lead for multi-client coordination                             |
| Portfolio Assessment                   | Rapid evaluation of which clients are affected/at risk                    |
| Coordinated Containment                | Common containment action applied across affected clients                 |
| Per-Client Tenant Handling             | Individual incident handling within each client's tenant                  |
| Sanitized Cross-Client Brief           | Anonymized intelligence shared across SOC for portfolio defense           |
| Campaign                               | Coordinated attack series typically by single threat actor                |
| Vulnerability-Driven Incident          | Incident caused by exploitation of common vulnerability                   |
| Coordinated Disclosure                 | Joint regulatory or public disclosure (rare)                              |

---

# 5. Roles and Responsibilities

## 5.1 Core MSSP Roles

| Role                                       | Responsibilities                                                       |
| ------------------------------------------ | ---------------------------------------------------------------------- |
| **Cross-Client Incident Commander (CCIC)** | Overall coordination; portfolio-level decisions; communication aligned |
| **MSSP SOC Manager**                       | Resource allocation; CCIC appointment; executive escalation            |
| **MSSP IR Team Lead**                      | Technical investigation coordination                                   |
| **Per-Client SDM**                         | Per-client communication; per-client decisions; tenant integrity       |
| **Per-Client SOC Analysts**                | Per-tenant investigation and response (assigned analysts only)         |
| **Threat Intel Lead**                      | Cross-client correlation; sanitized intel briefs                       |
| **Detection Engineer**                     | Portfolio-wide detection deployment                                    |
| **Compliance Lead**                        | Per-client regulatory assessment and reporting                         |
| **MSSP CISO**                              | Strategic oversight; executive engagement; portfolio decisions         |

## 5.2 Per-Client Roles

| Role                       | Per-Client Responsibilities                                 |
| -------------------------- | ----------------------------------------------------------- |
| **Client SDM**             | Single liaison per client; never coordinates across clients |
| **Client Analyst Team**    | Tenant-scoped investigation only                            |
| **Client Primary Contact** | Receives client-specific notifications                      |
| **Client CISO**            | Per-client decisions                                        |

References:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`

---

# 6. Cross-Client Principles (Mandatory)

| Principle                            | Requirement                                                     |
| ------------------------------------ | --------------------------------------------------------------- |
| **Tenant Segregation Above All**     | No cross-tenant data sharing without sanitization               |
| **Per-Client Incident Records**      | Each affected client gets own incident ticket                   |
| **Portfolio Coordination via CCIC**  | Single coordinator; never analyst-to-analyst cross-client       |
| **Sanitized Intelligence Sharing**   | Internal cross-client briefs always sanitized                   |
| **Per-Client Communication**         | Each client communicated separately; consistent message         |
| **Per-Client Authority**             | Each client retains decision authority for their tenant         |
| **No Disclosure Across Clients**     | Affected client list never shared with any client               |
| **Coordinated Detection Deployment** | Detection rules deployed to all (after sanitization)            |
| **Per-Client Regulatory Reporting**  | Each client handles own regulatory obligations                  |
| **Sanitized Lessons Learned**        | Aggregated learnings sanitized before sharing                   |
| **Audit Trail**                      | All cross-client coordination logged with sanitization evidence |

---

# 7. Cross-Client Incident Triggers (Mandatory)

The following conditions trigger cross-client incident procedures:

## 7.1 Automatic Triggers

| Trigger                                                      | Threshold        |
| ------------------------------------------------------------ | ---------------- |
| Same IoC detected across ≥2 clients in 24 hours              | Auto-correlation |
| Same CVE exploitation attempted across ≥2 clients in 7 days  | Auto-correlation |
| Same threat actor TTP confirmed across ≥2 clients in 30 days | Auto-correlation |
| Same supply chain provider compromise affecting ≥2 clients   | Auto-trigger     |
| Same SaaS provider incident affecting ≥2 clients             | Auto-trigger     |

## 7.2 Manual Triggers

| Trigger                                                        | Owner              |
| -------------------------------------------------------------- | ------------------ |
| External advisory (CERT-In, vendor) affecting MSSP client base | Threat Intel Lead  |
| Critical vulnerability with portfolio-wide exposure            | Detection Engineer |
| Pattern observed by senior analyst across clients              | L3 Analyst → CCIC  |
| Industry/regulator alert relevant to client base               | Compliance Lead    |

---

# 8. Cross-Client Incident Severity (Mandatory)

| Cross-Client Severity | Definition                                                     | CCIC Required?             |
| --------------------- | -------------------------------------------------------------- | -------------------------- |
| **XC-P1 (Critical)**  | ≥3 clients affected OR ≥1 P1 incident OR active exploitation   | Yes                        |
| **XC-P2 (High)**      | 2 clients affected OR P2 incidents OR active threat campaign   | Yes                        |
| **XC-P3 (Medium)**    | 2+ clients at risk (no active exploitation) OR emerging threat | Yes (lightweight)          |
| **XC-P4 (Low)**       | Portfolio-wide informational; no active incidents              | No (Threat Intel briefing) |

---

# 9. Cross-Client Incident Lifecycle (Mandatory)

```
┌──────────────────────────────────────────────────────────┐
│  Phase 1: DETECTION & CORRELATION                        │
│  Identify pattern across clients                         │
└──────────────────────────────────────────────────────────┘
                          │
                          ▼
┌──────────────────────────────────────────────────────────┐
│  Phase 2: PORTFOLIO ASSESSMENT                           │
│  CCIC appointed; affected/at-risk clients identified     │
└──────────────────────────────────────────────────────────┘
                          │
                          ▼
┌──────────────────────────────────────────────────────────┐
│  Phase 3: PER-CLIENT INCIDENT ESTABLISHMENT              │
│  Individual tickets created per affected client          │
└──────────────────────────────────────────────────────────┘
                          │
                          ▼
┌──────────────────────────────────────────────────────────┐
│  Phase 4: COORDINATED RESPONSE                           │
│  Per-client containment; portfolio-level coordination    │
└──────────────────────────────────────────────────────────┘
                          │
                          ▼
┌──────────────────────────────────────────────────────────┐
│  Phase 5: PER-CLIENT COMMUNICATION                       │
│  Each client notified individually; sanitized intel      │
└──────────────────────────────────────────────────────────┘
                          │
                          ▼
┌──────────────────────────────────────────────────────────┐
│  Phase 6: PORTFOLIO-WIDE PROTECTION                      │
│  Detection rules deployed; preventive measures           │
└──────────────────────────────────────────────────────────┘
                          │
                          ▼
┌──────────────────────────────────────────────────────────┐
│  Phase 7: PER-CLIENT REGULATORY REPORTING                │
│  Each client reports per own obligations                 │
└──────────────────────────────────────────────────────────┘
                          │
                          ▼
┌──────────────────────────────────────────────────────────┐
│  Phase 8: PER-CLIENT CLOSURE                             │
│  Each client incident closed independently               │
└──────────────────────────────────────────────────────────┘
                          │
                          ▼
┌──────────────────────────────────────────────────────────┐
│  Phase 9: PORTFOLIO LESSONS LEARNED                      │
│  Sanitized aggregated learnings; master playbook updates │
└──────────────────────────────────────────────────────────┘
```

---

# 10. Phase 1: Detection & Correlation (Mandatory)

## 10.1 Correlation Methods

| Method                             | Source                                   | Owner                |
| ---------------------------------- | ---------------------------------------- | -------------------- |
| Cross-tenant IoC correlation       | TI Platform aggregation                  | Threat Intel Analyst |
| Cross-tenant TTP correlation       | SOC analyst observation; L3 review       | L3 Analyst           |
| Cross-tenant alert pattern         | SOAR/SIEM aggregate analytics            | Detection Engineer   |
| External advisory correlation      | CERT-In/vendor advisories vs client base | Threat Intel Analyst |
| Vulnerability scanning correlation | Common CVE across client environments    | Compliance Lead      |
| Manual analyst escalation          | Direct observation                       | Any analyst → CCIC   |

## 10.2 Correlation Constraints

| Constraint                    | Requirement                                                              |
| ----------------------------- | ------------------------------------------------------------------------ |
| **Aggregation-only view**     | Correlation views must aggregate; never expose individual client details |
| **Analyst access**            | Only Threat Intel Lead + Detection Eng + CCIC have aggregated view       |
| **Client identifiers hidden** | Use tenant IDs; never client names in correlation views                  |
| **Audit logging**             | All correlation queries logged                                           |

## 10.3 Initial Correlation Output

When pattern detected, document:

| Field                                   | Value                         |
| --------------------------------------- | ----------------------------- |
| Correlation ID                          | `XC-COR-YYYY-####`            |
| Detection date/time (UTC)               |                               |
| Detection method                        |                               |
| Pattern description                     |                               |
| Number of tenants affected (count only) |                               |
| Tenant IDs (internal reference)         |                               |
| Severity recommendation                 | XC-P1 / XC-P2 / XC-P3 / XC-P4 |
| Recommended CCIC                        |                               |
| Initial assessment by                   |                               |

---

# 11. Phase 2: Portfolio Assessment (Mandatory)

## 11.1 CCIC Appointment

When correlation confirms cross-client incident:

| Step | Action                               | Owner                   | Timeline                      |
| ---- | ------------------------------------ | ----------------------- | ----------------------------- |
| 1    | Correlation escalated to SOC Manager | TI Lead / Detection Eng | Within 15 min                 |
| 2    | CCIC appointed                       | SOC Manager             | Within 30 min (XC-P1: 15 min) |
| 3    | CCIC briefing                        | SOC Manager             | Within 1 hour                 |
| 4    | War room activated (XC-P1/P2)        | CCIC                    | Within 1 hour                 |

### 11.1.1 CCIC Selection Criteria

| Severity | Typical CCIC Role               |
| -------- | ------------------------------- |
| XC-P1    | IR Team Lead or SOC Manager     |
| XC-P2    | IR Team Lead or Senior L3       |
| XC-P3    | Senior L3 or Detection Eng Lead |
| XC-P4    | Threat Intel Lead               |

## 11.2 Portfolio Impact Assessment

CCIC conducts portfolio assessment:

| Assessment Element                       | Details                           |
| ---------------------------------------- | --------------------------------- |
| Total affected clients                   | Confirmed by tenant ID            |
| At-risk clients (not yet affected)       | Based on environment profile      |
| Affected client severity per tenant      | Tenant-scoped severity            |
| Critical infrastructure clients affected | BFSI / Healthcare / CII           |
| Regulatory exposure                      | RBI / CERT-In / sector regulators |
| Common threat vector                     | IoC / CVE / TTP / Vendor / SaaS   |
| Active exploitation status               | Active / Attempted / Theoretical  |
| Estimated portfolio business impact      | Aggregated                        |

## 11.3 Per-Client Risk Categorization

For each potentially affected client:

| Status                 | Definition                              | Action                         |
| ---------------------- | --------------------------------------- | ------------------------------ |
| **Confirmed Affected** | Active compromise detected              | Per-client P1/P2 incident      |
| **Likely Affected**    | Strong indicators; not yet confirmed    | Per-client P2 investigation    |
| **At Risk**            | Exposed but no indicators of compromise | Per-client preventive measures |
| **Not At Risk**        | Environment not exposed to threat       | Monitor only; no action        |

---

# 12. Phase 3: Per-Client Incident Establishment (Mandatory)

## 12.1 Tenant-Scoped Ticket Creation

For each affected client:

| Action                                      | Owner                     | Note                                   |
| ------------------------------------------- | ------------------------- | -------------------------------------- |
| Create per-client incident ticket           | Per-client SDM            | Tenant-scoped                          |
| Assign per-client severity                  | Per-client SDM + SOC Lead | Per client environment impact          |
| Link to internal CCIC reference (sanitized) | CCIC                      | No cross-client visibility to analysts |
| Notify client per standard escalation       | Per-client SDM            | Per client SLA                         |
| Assign tenant-scoped analyst team           | SOC Manager               | Per analyst assignment                 |
| Initiate tenant-scoped investigation        | Per-client analysts       | Per client playbooks                   |

## 12.2 Cross-Reference Restrictions

| Rule                                                     | Requirement     |
| -------------------------------------------------------- | --------------- |
| Per-client tickets must NOT reference other client names | Strict          |
| Per-client tickets may reference internal CCIC ID        | Allowed         |
| Per-client tickets may reference sanitized threat brief  | Allowed         |
| Analysts must NOT see other clients' tickets             | RBAC enforced   |
| SDMs must NOT discuss with other SDMs except via CCIC    | Process control |

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 13. Phase 4: Coordinated Response (Mandatory)

## 13.1 CCIC Coordination Cell

CCIC operates a coordination cell consisting of:

| Participant        | Role                                                  |
| ------------------ | ----------------------------------------------------- |
| CCIC               | Overall coordination                                  |
| Threat Intel Lead  | Intelligence updates                                  |
| Detection Engineer | Detection deployment                                  |
| Compliance Lead    | Regulatory tracking                                   |
| Per-client SDMs    | Per-client status updates (anonymized in shared cell) |
| SOC Manager        | Resource and escalation                               |

### 13.1.1 Coordination Cell Operating Rules

- Per-client SDMs report status using tenant IDs (not names) in shared cell
- Detailed per-client info shared only bilaterally with CCIC
- All cell communications logged
- No client-specific information shared between SDMs

## 13.2 Per-Client Response

Each per-client incident follows standard tenant-scoped playbook:

| Activity                           | Tenant-Scoped Owner          |
| ---------------------------------- | ---------------------------- |
| Triage                             | Per-client L1/L2             |
| Investigation                      | Per-client L2/L3             |
| Containment (per client authority) | Per-client SDM + Client CISO |
| Eradication                        | Per-client team              |
| Recovery                           | Per-client team              |
| Communication to client            | Per-client SDM               |
| Per-client regulatory reporting    | Per-client SDM + Compliance  |

## 13.3 Portfolio-Level Coordinated Actions

CCIC coordinates portfolio-level actions:

| Action                     | CCIC Decision                       | Per-Client Action                              |
| -------------------------- | ----------------------------------- | ---------------------------------------------- |
| Generic IoC blocking       | Approve portfolio-wide deployment   | Detection Eng deploys to all tenants           |
| CVE patching priority      | Recommend portfolio-wide priority   | Per-client SDM communicates to client          |
| Vendor coordination        | Joint vendor escalation (sanitized) | Vendor briefed with sanitized portfolio impact |
| External advisory issuance | CISO approval                       | Threat Intel publishes sanitized advisory      |
| Detection rule deployment  | Approve cross-portfolio rule        | Detection Eng deploys to all clients           |

References:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

# 14. Phase 5: Per-Client Communication (Mandatory)

## 14.1 Communication Principles

| Principle                       | Requirement                            |
| ------------------------------- | -------------------------------------- |
| Each client notified separately | Never CC multiple clients              |
| Consistent core message         | Aligned facts and recommendations      |
| Per-client customization        | Specific impact and authorities        |
| No disclosure of other clients  | Never reference other affected clients |
| Sanitized intel briefs          | Generic threat description             |
| Timeline alignment              | Coordinated communication windows      |

## 14.2 Standard Communication Template (Per Client)

CCIC drafts a sanitized core message; SDMs customize per client:

### 14.2.1 Core Message Elements

| Element                     | Content                                     |
| --------------------------- | ------------------------------------------- |
| Threat description          | Generic (no client attribution)             |
| Indicators                  | Sanitized IoCs                              |
| Recommended actions         | Generic and client-specific                 |
| Detection deployment status | "Deployed across our monitoring" (no count) |
| Vendor coordination status  | Generic update                              |
| Next update timing          |                                             |

### 14.2.2 Per-Client Customization

| Element                               | Per-Client Additions |
| ------------------------------------- | -------------------- |
| Client's specific affected systems    |                      |
| Client's specific severity            |                      |
| Client's specific containment actions |                      |
| Client's regulatory obligations       |                      |
| Client-specific escalation status     |                      |

References:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md`

## 14.3 Communication Cadence

| Severity | Update Frequency                    |
| -------- | ----------------------------------- |
| XC-P1    | Every 30-60 min during active phase |
| XC-P2    | Every 2-4 hours                     |
| XC-P3    | Daily                               |
| XC-P4    | Once (advisory)                     |

---

# 15. Phase 6: Portfolio-Wide Protection (Mandatory)

## 15.1 Detection Deployment

| Detection Type            | Deployment Scope                | Approval           |
| ------------------------- | ------------------------------- | ------------------ |
| Generic IoC-based         | All client tenants              | Detection Eng Lead |
| Generic TTP-based         | All client tenants              | Detection Eng Lead |
| Sanitized signature-based | All client tenants              | Detection Eng Lead |
| Vulnerability-specific    | All affected/at-risk tenants    | Detection Eng Lead |
| Client-specific custom    | Only the specific client tenant | Per-client SDM     |

## 15.2 Preventive Measure Recommendations

| Measure                     | Communication                               |
| --------------------------- | ------------------------------------------- |
| Patch deployment            | All clients with affected versions notified |
| Configuration hardening     | All applicable clients notified             |
| Account/credential rotation | Affected/at-risk clients notified           |
| Network controls            | All applicable clients notified             |
| Workarounds                 | All applicable clients notified             |

## 15.3 Hunt Hypothesis Distribution

Sanitized hunt hypotheses distributed to all SOC analysts (without client attribution) for portfolio-wide proactive hunting.

References:
`03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Threat-Hunting-Procedures.md`

---

# 16. Phase 7: Per-Client Regulatory Reporting (Mandatory)

## 16.1 Per-Client Reporting Independence

| Principle                         | Requirement                        |
| --------------------------------- | ---------------------------------- |
| Each client reports independently | Client retains reporting authority |
| MSSP supports per client          | No joint reports                   |
| Per-client timelines              | Per client regulatory obligations  |
| MSSP provides per-client evidence | Tenant-scoped                      |
| Sanitized threat context provided | Generic threat information         |

## 16.2 Regulatory Timeline Coordination

| Regulator                    | Per-Client Timeline         | MSSP Role           |
| ---------------------------- | --------------------------- | ------------------- |
| CERT-In                      | 6 hours per affected client | Support each client |
| RBI (per BFSI client)        | 2-6 hours per client        | Support each client |
| NCIIPC (per CII client)      | Per guidelines per client   | Support each client |
| Sector-specific (SEBI/IRDAI) | Per regulations             | Support each client |
| Privacy authorities (DPDP)   | Per Act timeline            | Support each client |

References:
`07_REPORTING/07.4_Regulatory-Reports/RBI-Mandatory-Report-Template.md`
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`

## 16.3 Sanitized External Advisory (Optional)

If MSSP issues public advisory (CISO approval required):

- Generic threat description
- No client attribution (no names, no count, no industry concentration)
- Defensive recommendations
- Approved by MSSP CISO + Legal

---

# 17. Phase 8: Per-Client Closure (Mandatory)

Each per-client incident closes independently:

| Closure Activity                       | Per-Client                 | Cross-Client                         |
| -------------------------------------- | -------------------------- | ------------------------------------ |
| Per-client containment confirmed       | Yes                        | Tracked by CCIC (aggregate)          |
| Per-client eradication confirmed       | Yes                        | Tracked by CCIC                      |
| Per-client recovery validated          | Yes                        | Tracked by CCIC                      |
| Per-client regulatory reporting closed | Yes                        | N/A                                  |
| Per-client RCA initiated               | Yes                        | Per client RCA                       |
| Per-client ticket closure              | Yes                        | Cross-client ticket closure separate |
| Cross-client ticket closure            | When all per-client closed | Yes                                  |

---

# 18. Phase 9: Portfolio Lessons Learned (Mandatory)

## 18.1 Aggregated Lessons Learned

| Activity                            | Owner                    | Timeline                      |
| ----------------------------------- | ------------------------ | ----------------------------- |
| Per-client LL sessions              | Per-client SDM + IR Lead | Per standard timelines        |
| Aggregated portfolio LL             | CCIC + SOC Manager       | Within 30 days                |
| Sanitized portfolio brief           | Threat Intel Lead        | Within 30 days                |
| Master playbook updates             | IR Team Lead             | Per Playbook Update Log       |
| Detection rule updates              | Detection Eng            | Per Detection Improvement Log |
| External knowledge sharing (if any) | CISO approval            | Per discretion                |

References:
`08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`
`08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

## 18.2 Sanitization for Portfolio LL

| Element                  | Sanitization Standard                                      |
| ------------------------ | ---------------------------------------------------------- |
| Client names             | Removed                                                    |
| Industry attribution     | Generalized (e.g., "BFSI clients") only if non-identifying |
| Client count             | Approximate ranges only (e.g., "multiple clients")         |
| Specific systems         | Generic descriptions                                       |
| Specific business impact | Generic impact categories                                  |
| Customer data references | Removed                                                    |

---

# 19. Cross-Client Incident Documentation (Mandatory)

## 19.1 CCIC Master Tracker

| Field                          | Description                           |
| ------------------------------ | ------------------------------------- |
| Cross-Client Incident ID       | `XC-INC-YYYY-####`                    |
| Date detected (UTC)            |                                       |
| Detection method               |                                       |
| Severity                       | XC-P1 / XC-P2 / XC-P3 / XC-P4         |
| CCIC                           |                                       |
| Total affected clients (count) |                                       |
| Total at-risk clients (count)  |                                       |
| Confirmed exploitation?        | Yes / No                              |
| Threat type                    | CVE / Actor / Vendor / SaaS / Pattern |
| Threat reference               | CVE-ID / Actor name / Vendor name     |
| Per-client incident IDs        | Internal reference (tenant IDs)       |
| Portfolio-wide actions taken   |                                       |
| Sanitized brief reference      |                                       |
| Status                         | Active / Contained / Closed           |
| Closure date (UTC)             |                                       |

## 19.2 Audit Trail Requirements

All cross-client activities must be logged with:

- Timestamp (UTC)
- Actor (role + person)
- Action (with sanitization status)
- Approval (where applicable)
- Justification

---

# 20. Cross-Client Roles Quick Reference (Mandatory)

| Role                   | Cross-Client Authority | Tenant Access         | Communication Authority    |
| ---------------------- | ---------------------- | --------------------- | -------------------------- |
| **CCIC**               | Full coordination      | Aggregate views only  | Internal MSSP only         |
| **MSSP CISO**          | Strategic decisions    | All (audit-logged)    | Executive escalations      |
| **SOC Manager**        | Resource allocation    | All (audit-logged)    | Internal MSSP only         |
| **Threat Intel Lead**  | Correlation analysis   | Aggregate + sanitized | Sanitized briefs           |
| **Detection Engineer** | Portfolio detection    | Detection scope only  | Sanitized rule advisories  |
| **Per-Client SDM**     | Per-client only        | Assigned client only  | Per-client client comms    |
| **Per-Client Analyst** | Per-client only        | Assigned client only  | None cross-client          |
| **Compliance Lead**    | Per-client tracking    | All (audit-logged)    | Per-client regulatory only |

---

# 21. Common Pitfalls to Avoid (Mandatory)

| Pitfall                                           | Mitigation                                          |
| ------------------------------------------------- | --------------------------------------------------- |
| Analyst-to-analyst cross-client discussion        | All coordination via CCIC only                      |
| Mentioning Client A while briefing Client B       | Strict sanitization                                 |
| Joint regulatory reports                          | Per-client reporting always                         |
| Sending mass email with multiple clients in TO/CC | Per-client emails only                              |
| Sharing screenshots with other client visible     | Sanitize before sharing                             |
| Bridge call with multiple clients                 | Never; per-client bridges only                      |
| Inferring affected count to clients               | Generic statements only                             |
| Detection rules with client-specific data         | Sanitize before portfolio deployment                |
| Skipping per-client LL because cross-client done  | Both required                                       |
| Late CCIC appointment                             | Auto-correlation triggers must escalate immediately |

---

# 22. Quality Checklist (Per Cross-Client Incident)

Before closing a cross-client incident:

- [ ] CCIC appointed within timeline
- [ ] Portfolio assessment completed
- [ ] All affected clients identified
- [ ] Per-client incident tickets created
- [ ] Tenant segregation maintained throughout
- [ ] Coordination cell operated per process
- [ ] Detection rules deployed portfolio-wide
- [ ] Per-client communications completed
- [ ] No cross-client information leakage
- [ ] Per-client regulatory reporting supported
- [ ] All per-client incidents closed independently
- [ ] Aggregated portfolio LL completed
- [ ] Sanitized brief published
- [ ] Master playbook updates initiated (if applicable)
- [ ] Detection improvements logged
- [ ] Audit trail complete
- [ ] CISO sign-off (XC-P1/XC-P2)

---

# 23. Training and Exercises (Mandatory)

| Training                             | Audience                            | Frequency |
| ------------------------------------ | ----------------------------------- | --------- |
| Cross-client procedure training      | All SOC personnel                   | Annually  |
| CCIC role training                   | IR Team Lead + Senior L3            | Annually  |
| Sanitization training                | Threat Intel + Detection Eng + SDMs | Annually  |
| Cross-client tabletop exercise       | Full SOC                            | Annually  |
| Multi-tenant supply chain simulation | Full SOC + Threat Intel             | Annually  |

References:
`10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/`

---

# 24. Integration with Other Processes

| Process                        | Integration                                |
| ------------------------------ | ------------------------------------------ |
| Multi-Client Alert Handling    | Initial detection feeds into correlation   |
| Client Data Segregation Policy | Enforced throughout                        |
| Per-Client Playbooks           | Used for tenant-scoped handling            |
| Threat Intelligence (TI)       | Correlation engine and brief output        |
| Detection Engineering          | Portfolio-wide rule deployment             |
| Regulatory Reporting           | Per-client reporting orchestration         |
| Lessons Learned                | Aggregated + per-client                    |
| Playbook Update Log            | Master updates from cross-client learnings |
| Detection Improvement Log      | Portfolio detection improvements           |
| Steering Committee Reporting   | Sanitized portfolio metrics                |

---

# 25. Related Documents

| Document                       | Path                                                                                     |
| ------------------------------ | ---------------------------------------------------------------------------------------- |
| Client Data Segregation Policy | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`        |
| Multi-Client Alert Handling    | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`           |
| Client Environment Profile     | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`         |
| Client IR Contacts             | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`                          |
| Client-Specific Playbook Guide | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/Client-Specific-Playbook-Guide.md`  |
| MSSP ISO27001 Controls         | `09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-ISO27001-Controls.md`                        |
| MSSP Audit Readiness Checklist | `09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-Audit-Readiness-Checklist.md`                |
| TTP Intelligence Report        | `08_POST-INCIDENT/08.4_Threat-Intel-Output/TTP-Intelligence-Report.md`                   |
| IoC Output Register            | `08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md`                       |
| Threat Actor Profile Template  | `08_POST-INCIDENT/08.4_Threat-Intel-Output/Threat-Actor-Profile-Template.md`             |
| Supply Chain Master Playbook   | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-Master.md`                         |
| Zero-Day Master Playbook       | `02_PLAYBOOKS/02.12_Zero-Day-Exploit/PB-ZeroDay-Master.md`                               |
| APT Master Playbook            | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Master.md`                                       |
| Detection Improvement Log      | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`                |
| Playbook Update Log            | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`                      |
| RBI Mandatory Report Template  | `07_REPORTING/07.4_Regulatory-Reports/RBI-Mandatory-Report-Template.md`                  |
| CERT-In Reporting SOP          | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md` |
| L2 Threat Hunting Procedures   | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Threat-Hunting-Procedures.md`              |
| Tabletop Exercise Guide        | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`           |

---

# 26. Revision History

| Version | Date        | Author                          | Changes         |
| ------- | ----------- | ------------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP SOC Manager / IR Team Lead | Initial version |

---

# 27. Approval

Approved by:

| Role                 | Name | Signature | Date |
| -------------------- | ---- | --------- | ---- |
| MSSP SOC Manager     |      |           |      |
| MSSP IR Team Lead    |      |           |      |
| MSSP Compliance Lead |      |           |      |
| MSSP CISO            |      |           |      |

---

**End of Document**
