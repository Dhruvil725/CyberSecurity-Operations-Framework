# Client Escalation Matrix (Client-Specific)

---

# 1. Document Control

| Field                | Value                                           |
| -------------------- | ----------------------------------------------- |
| Document Name        | Client Escalation Matrix – [CLIENT-NAME]        |
| Document ID          | MSSP-CL-ESC-[CLIENT-ID]                         |
| Version              | 1.0                                             |
| Effective Date       | `[YYYY-MM-DD]`                                  |
| Client Name          | `[CLIENT-NAME]`                                 |
| Client ID            | `CL-####`                                       |
| Owner (MSSP)         | MSSP SDM / SOC Manager                          |
| Owner (Client)       | Client CISO / Security Lead                     |
| Approved By (MSSP)   | MSSP SOC Manager                                |
| Approved By (Client) | Client CISO                                     |
| Classification       | Confidential – Client Restricted                |
| Review Cycle         | Quarterly (or upon contact / structural change) |

---

# 2. Purpose

This document defines the **Client-Specific Escalation Matrix** for `[CLIENT-NAME]`, providing the authoritative, time-bound escalation paths used during incident response, operational events, SLA breaches, and crisis situations involving both MSSP and client teams.

A formal client escalation matrix is critical because:

- timely escalation is the single most important factor in containing impact during P1/P2 incidents
- incorrect or delayed escalation directly causes SLA breaches and regulatory non-compliance
- NIST CSF Respond (RS.CO) function requires structured escalation and communication
- ISO 27001 Annex A.5.24 requires planned response with defined roles
- RBI Cyber Security Framework expects defined escalation per incident severity
- multi-tenant MSSP operations require client-specific escalation isolated from other clients
- audit and inspection require evidence of escalation matrix maintenance and execution
- analysts under pressure during P1 need clear, unambiguous escalation paths
- 24x7 coverage requires primary, backup, and emergency-override contacts
- regulatory reportable incidents trigger time-bound escalations (RBI 2-6 hr, CERT-In 6 hr)
- crisis bridge calls require pre-defined participants per incident type
- joint MSSP-client governance requires escalation aligned across both organizations
- this matrix operationalizes the Client IR Policy escalation framework

This matrix ensures:

- unambiguous escalation paths per incident severity and category
- time-bound reach SLAs at each escalation level
- defined approval authorities at each level
- 24x7 coverage with primary, backup, and emergency contacts
- specialized escalation paths for regulatory, legal, HR, crisis, and customer-impact scenarios
- audit-ready evidence of escalation governance
- tenant segregation from other client escalation matrices
- linkage to Client IR Policy, Client IR Contacts, and client-specific playbooks

Reference alignment:
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/Client-IR-Policy.md`
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md`

---

# 3. Scope

This matrix applies to escalations involving:

| Escalation Trigger                | Examples                                       |
| --------------------------------- | ---------------------------------------------- |
| Incident severity escalation      | P3 → P2 → P1 progression                       |
| SLA breach / risk of breach       | Acknowledgement, response, resolution SLAs     |
| Containment authority decisions   | Actions requiring client approval              |
| Regulatory reportable incidents   | RBI / CERT-In / sector reportable              |
| Crisis activation                 | Material incidents, customer impact, media     |
| Legal hold / litigation risk      | Insider threat, data breach, regulatory action |
| HR-coordinated incidents          | Insider threat, employee misconduct            |
| Customer-impacting incidents      | Service disruption, data exposure              |
| Executive/board notification      | Material incidents, regulatory reporting       |
| Vendor / third-party coordination | Supply chain, vendor incidents                 |
| Cyber insurance engagement        | Claim-triggering incidents                     |
| Out-of-hours coverage             | After-hours P1/P2                              |

Out of scope:

- Routine BAU operational escalations not affecting client
- MSSP-internal escalations not involving client
- Generic master escalation paths (covered in `Escalation-Matrix-Master.md`)

---

# 4. Definitions

| Term               | Definition                                        |
| ------------------ | ------------------------------------------------- |
| Escalation         | Movement of issue/decision up the authority chain |
| Escalation Trigger | Specific condition initiating escalation          |
| Reach SLA          | Maximum time to successfully establish contact    |
| Primary Contact    | First person contacted at given level             |
| Backup Contact     | Second person if primary unreachable              |
| Emergency Override | Process when standard escalation fails            |
| Crisis Bridge      | Live conference bridge for major incidents        |
| Acknowledgement    | Confirmation of receipt and ownership             |
| Response           | Active engagement and progress                    |
| Escalation Path    | Ordered sequence of contacts                      |
| Authority Level    | Decision-making power per role                    |
| War Room           | Physical or virtual incident command center       |

---

# 5. Roles and Responsibilities

## 5.1 MSSP Roles in Escalation

| Role              | Escalation Responsibilities                           |
| ----------------- | ----------------------------------------------------- |
| MSSP L1 Analyst   | Detect, triage, initiate escalation per criteria      |
| MSSP L2 Analyst   | Investigate, escalate to L3, engage client primary    |
| MSSP L3 Analyst   | Deep investigation, escalate to IR Team Lead          |
| MSSP SOC Lead     | Approve escalations, coordinate bridge, notify client |
| MSSP IR Team Lead | Lead joint IR, escalate to SOC Manager                |
| MSSP SOC Manager  | Engage client CISO, executive escalation              |
| MSSP CISO         | Engage client executive, strategic decisions          |
| MSSP SDM          | Coordinate all client communications                  |

## 5.2 Client Roles in Escalation

| Role                     | Escalation Responsibilities                         |
| ------------------------ | --------------------------------------------------- |
| Client Primary Contact   | Receive routine escalations, coordinate client side |
| Client 24x7 On-Call      | Receive after-hours P1/P2 escalations               |
| Client Security Lead     | Receive L2-level escalations, technical decisions   |
| Client CISO              | Receive L3/Mgmt escalations, strategic decisions    |
| Client CIO               | IT operational decisions, infrastructure changes    |
| Client Executive Sponsor | Business decisions, material incidents              |
| Client CEO/MD            | Material incident sign-off, regulatory authority    |
| Client Compliance        | Regulatory reporting decisions                      |
| Client Legal             | Legal hold, external communications                 |
| Client HR                | Insider threat coordination                         |
| Client Communications    | Internal/external/customer comms                    |

References:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`

---

# 6. Escalation Principles (Mandatory)

| Principle         | Requirement                                  |
| ----------------- | -------------------------------------------- |
| Time-bound        | Every level has Reach SLA                    |
| Multi-channel     | Phone + Email + Mobile minimum               |
| Primary + Backup  | Every position has both                      |
| 24x7 coverage     | After-hours paths explicit                   |
| Documented        | All escalations logged in ticket             |
| Acknowledged      | Receipt confirmation required                |
| Pre-authorized    | Common decisions pre-approved to avoid delay |
| Auditable         | Complete trail maintained                    |
| Tested            | Annual validation via drills                 |
| Tenant-segregated | No cross-client escalation paths             |

---

# 7. General Escalation Flow (Reference)

```
┌──────────────────────────────────────────────────────────┐
│                  INCIDENT DETECTED                       │
└──────────────────────────────────────────────────────────┘
                          │
                          ▼
          ┌───────────────────────────────┐
          │     MSSP L1 TRIAGE            │
          │   (Reach SLA: per SLA)        │
          └───────────────────────────────┘
                          │
              ┌───────────┴───────────┐
              ▼                       ▼
        ┌──────────┐            ┌──────────┐
        │ P3 / P4  │            │ P1 / P2  │
        └──────────┘            └──────────┘
              │                       │
              ▼                       ▼
        Logged for       ┌─────────────────────────┐
        routine          │   MSSP L2 ESCALATION    │
        handling         │  + Client Primary       │
                         │  + Client Security Lead │
                         └─────────────────────────┘
                                     │
                                     ▼
                         ┌─────────────────────────┐
                         │   MSSP L3 / IR LEAD     │
                         │  + Client CISO          │
                         └─────────────────────────┘
                                     │
                            P1 / Material
                                     │
                                     ▼
                         ┌─────────────────────────┐
                         │   MSSP SOC MGR + CISO   │
                         │  + Client CIO / CEO     │
                         │  + Crisis Bridge        │
                         │  + Regulatory Reporting │
                         └─────────────────────────┘
```

---

# 8. Severity-Based Escalation Matrix (Mandatory)

## 8.1 P1 (Critical) Escalation Matrix

| Level | Contact (MSSP)        | Contact (Client)               | Reach SLA | Trigger                          | Decision Authority     |
| ----- | --------------------- | ------------------------------ | --------- | -------------------------------- | ---------------------- |
| 1     | L1 Analyst (on-shift) | —                              | Immediate | Detection / Alert                | Triage                 |
| 2     | L2/L3 Analyst         | Client Primary Contact (24x7)  | 5 min     | P1 confirmed                     | Investigation lead     |
| 3     | SOC Lead              | Client Security Lead           | 10 min    | P1 declared                      | Containment approval   |
| 4     | IR Team Lead          | Client CISO                    | 15 min    | P1 confirmed material risk       | Strategic IR decisions |
| 5     | SOC Manager + SDM     | Client CIO + Executive Sponsor | 30 min    | Material incident threshold      | Business/IT decisions  |
| 6     | MSSP CISO             | Client CEO/MD                  | 1 hour    | Regulatory reportable / Material | Executive sign-off     |

### 8.1.1 P1 Mandatory Actions

| Action                        | Owner           | Timeline      |
| ----------------------------- | --------------- | ------------- |
| Open P1 ticket                | L1 Analyst      | Immediate     |
| Notify client primary contact | L1/L2 Analyst   | Within 5 min  |
| Activate crisis bridge        | SOC Lead        | Within 15 min |
| Notify CISO (both sides)      | SOC Lead        | Within 15 min |
| Notify executive sponsor      | SDM             | Within 30 min |
| Containment initiated         | IR Team Lead    | Per playbook  |
| Regulatory assessment         | Compliance Lead | Within 1 hour |
| First status update           | SDM             | Within 30 min |
| Subsequent updates            | SDM             | Every 30 min  |

---

## 8.2 P2 (High) Escalation Matrix

| Level | Contact (MSSP)             | Contact (Client)       | Reach SLA | Trigger                      | Decision Authority  |
| ----- | -------------------------- | ---------------------- | --------- | ---------------------------- | ------------------- |
| 1     | L1 Analyst                 | —                      | Immediate | Detection                    | Triage              |
| 2     | L2 Analyst                 | Client Primary Contact | 15 min    | P2 confirmed                 | Investigation lead  |
| 3     | L3 Analyst (if needed)     | Client Security Lead   | 30 min    | Investigation depth required | Technical analysis  |
| 4     | SOC Lead                   | Client CISO            | 1 hour    | Escalation criteria          | Strategic decisions |
| 5     | IR Team Lead / SOC Manager | Client CIO             | 2 hours   | If sustained / scope grows   | Business decisions  |

### 8.2.1 P2 Mandatory Actions

| Action                         | Owner      | Timeline        |
| ------------------------------ | ---------- | --------------- |
| Open P2 ticket                 | L1 Analyst | Within SLA      |
| Notify client primary          | L2 Analyst | Within 30 min   |
| Initial assessment             | L2 Analyst | Within 1 hour   |
| Status update                  | SDM        | Every 1-2 hours |
| Escalate to P1 if criteria met | SOC Lead   | Immediate       |

---

## 8.3 P3 (Medium) Escalation Matrix

| Level | Contact (MSSP) | Contact (Client)       | Reach SLA | Trigger                    | Decision Authority |
| ----- | -------------- | ---------------------- | --------- | -------------------------- | ------------------ |
| 1     | L1 Analyst     | —                      | Per SLA   | Detection                  | Triage             |
| 2     | L2 Analyst     | Client Primary Contact | 2 hours   | Investigation needed       | Investigation lead |
| 3     | SOC Lead       | Client Security Lead   | 4 hours   | If escalation criteria met | Decisions          |

### 8.3.1 P3 Standard Actions

| Action                          | Owner      | Timeline     |
| ------------------------------- | ---------- | ------------ |
| Open P3 ticket                  | L1 Analyst | Within SLA   |
| Daily summary notification      | SDM        | Daily report |
| Escalate to P2 if scope expands | SOC Lead   | Per criteria |

---

## 8.4 P4 (Low) Escalation Matrix

| Level        | Contact (MSSP) | Contact (Client)      | Reach SLA   |
| ------------ | -------------- | --------------------- | ----------- |
| 1            | L1 Analyst     | —                     | Per SLA     |
| Notification | —              | Weekly/Monthly report | Per cadence |

---

# 9. Scenario-Based Escalation Paths (Mandatory)

## 9.1 Containment Authority Escalation

For containment actions requiring client approval:

| Containment Action               | Escalation Required? | Contact                      |
| -------------------------------- | -------------------- | ---------------------------- |
| Endpoint isolation (single host) | Pre-approved         | None (execute)               |
| Endpoint isolation (mass >10)    | Yes                  | Client IT Lead → CISO        |
| Disable privileged account       | Yes                  | Client Identity Lead         |
| Block at internal firewall       | Yes                  | Client Network Lead          |
| Disable cloud account            | Yes                  | Client Cloud Lead            |
| Take application offline         | Yes                  | App Owner + Business Sponsor |
| Network segment isolation        | Yes                  | Client Network Lead + CISO   |

Reference: Containment Authority Matrix in `Client-IR-Policy.md`

---

## 9.2 Regulatory Reporting Escalation

| Trigger                         | Escalation Sequence                                            | Reach SLA                      |
| ------------------------------- | -------------------------------------------------------------- | ------------------------------ |
| Potential RBI reportable        | MSSP Compliance → Client Compliance → Client CISO → Client CEO | Within 1 hour of determination |
| CERT-In reportable (6-hr clock) | MSSP SOC Lead → Client Compliance → Client CISO                | Within 30 min of determination |
| NCIIPC reportable (if CII)      | Same as RBI                                                    | Within 1 hour                  |
| DPDP Act breach                 | MSSP Compliance → Client DPO → Client Legal → Client CISO      | Within 1 hour                  |
| Other regulatory (SEBI/IRDAI)   | MSSP Compliance → Client Compliance → Client CISO              | Within 1 hour                  |

References:
`07_REPORTING/07.4_Regulatory-Reports/RBI-Mandatory-Report-Template.md`
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 9.3 Legal / Litigation Risk Escalation

| Trigger                       | Escalation Sequence                                   | Reach SLA              |
| ----------------------------- | ----------------------------------------------------- | ---------------------- |
| Legal hold required           | MSSP SOC Manager → Client Legal Counsel → Client CISO | Within 1 hour          |
| Insider threat with HR action | MSSP IR Lead → Client HR + Legal + Security           | Within 2 hours         |
| External counsel needed       | Client Legal → External Counsel (client retains)      | Per client process     |
| Law enforcement engagement    | Client Legal → Client CISO → Law Enforcement          | Per client process     |
| Litigation hold               | Client Legal → MSSP SOC Manager                       | Immediate notification |

References:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`
`02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-HR-Legal-Coordination.md`

---

## 9.4 Customer-Impacting Incident Escalation

| Trigger                                  | Escalation Sequence                        | Reach SLA          |
| ---------------------------------------- | ------------------------------------------ | ------------------ |
| Service unavailability (customer-facing) | Client App Owner + Business Sponsor + CISO | Within 15 min      |
| Customer data exposure                   | Client DPO + Legal + CISO + Comms          | Within 30 min      |
| Customer notification required           | Client Communications + Legal + CISO       | Within 1 hour      |
| Customer helpline activation             | Client Customer Ops + Comms                | Per client process |

---

## 9.5 Crisis / Material Incident Escalation

| Trigger                         | Crisis Activation                          | Reach SLA     |
| ------------------------------- | ------------------------------------------ | ------------- |
| Material incident declared      | Joint Crisis Bridge                        | Within 30 min |
| Media inquiry received          | Client Communications + Legal + CISO + CEO | Within 30 min |
| Regulatory inspection triggered | Client Compliance + Legal + CISO + CEO     | Within 1 hour |
| Customer mass-impact            | Crisis Bridge + Customer Comms + Business  | Within 30 min |

### 9.5.1 Crisis Bridge Participants (Standard)

**MSSP Side:**

- SDM
- SOC Manager
- IR Team Lead
- L3 Analyst (lead investigator)
- Compliance Lead (if regulatory)

**Client Side:**

- Primary Contact
- Security Lead
- CISO
- CIO
- Executive Sponsor
- Legal Counsel (if needed)
- Communications (if needed)
- DPO (if data breach)
- Application Owner (if app-specific)

References:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Bridge-Call-Agenda-Template.md`

---

## 9.6 SLA Breach Escalation

| SLA Breach                      | Escalation Sequence             | Reach SLA     |
| ------------------------------- | ------------------------------- | ------------- |
| P1 acknowledgement SLA at risk  | SOC Lead → SOC Manager → SDM    | Immediate     |
| P1 acknowledgement SLA breached | SDM → Client Primary + CISO     | Within 5 min  |
| P2 acknowledgement SLA at risk  | SOC Lead                        | Immediate     |
| Response SLA at risk            | SOC Lead → SDM → Client Primary | Within 15 min |
| Resolution SLA at risk          | SOC Manager → SDM → Client CISO | Within 30 min |
| Multiple SLA breaches           | MSSP CISO → Client CISO         | Within 1 hour |

References:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLA-Breach-Escalation-Procedure.md`

---

## 9.7 Cyber Insurance Carrier Engagement

| Trigger                             | Escalation Sequence                                   |
| ----------------------------------- | ----------------------------------------------------- |
| Claim-triggering event (per policy) | Client Risk Mgmt → Insurance Carrier (client retains) |
| MSSP notification of incident       | Client to MSSP for evidence support                   |
| Insurance carrier requests          | Through Client SDM only                               |

---

## 9.8 Third-Party / Supply Chain Incident Escalation

| Trigger                          | Escalation Sequence                     |
| -------------------------------- | --------------------------------------- |
| Vendor incident affecting client | Client Vendor Mgmt + Security + CISO    |
| Supply chain compromise          | Client CISO + Executive Sponsor + Legal |
| Critical SaaS provider incident  | Client App Owner + Vendor Mgmt + CISO   |

References:
`02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-Vendor-Coordination.md`

---

# 10. Out-of-Hours / 24x7 Escalation (Mandatory)

## 10.1 After-Hours P1 Path

| Level                         | Primary Contact   | Backup Contact  | Reach SLA |
| ----------------------------- | ----------------- | --------------- | --------- |
| MSSP L2/L3 (24x7)             | On-shift L2/L3    | Backup L2/L3    | Immediate |
| MSSP SOC Lead (24x7)          | On-shift SOC Lead | Backup SOC Lead | 5 min     |
| MSSP IR Team Lead (on-call)   | Primary on-call   | Backup on-call  | 15 min    |
| Client 24x7 On-Call (Primary) | Per rotation      | Per rotation    | 15 min    |
| Client 24x7 On-Call (Backup)  | Per rotation      | Per rotation    | 15 min    |
| Client CISO (after-hours)     | Mobile            | EA / Alternate  | 30 min    |

## 10.2 Weekend / Holiday Coverage

- Same as after-hours
- Confirm coverage with client weekly for holidays
- Pre-defined alternate contacts for known leave periods

References:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`

---

# 11. Emergency Override (Mandatory)

When standard escalation paths fail (contacts unreachable):

| Sequence | Action                                                                                      |
| -------- | ------------------------------------------------------------------------------------------- |
| 1        | Attempt all primary + backup contacts (per directory)                                       |
| 2        | Document attempts with timestamps in ticket                                                 |
| 3        | Escalate to MSSP SOC Manager                                                                |
| 4        | MSSP CISO engages Client CISO directly                                                      |
| 5        | MSSP CISO engages Client Executive Sponsor                                                  |
| 6        | If material risk and no client response: MSSP executes pre-authorized emergency containment |
| 7        | Document all actions for post-incident review                                               |
| 8        | Post-incident: review escalation path effectiveness                                         |

References:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md`

---

# 12. Escalation Acknowledgement Standards (Mandatory)

| Level         | Acknowledgement Required Within | Channel                          |
| ------------- | ------------------------------- | -------------------------------- |
| P1 escalation | 5 minutes                       | Phone (verbal) + Email (written) |
| P2 escalation | 15 minutes                      | Email + Phone confirmation       |
| P3 escalation | 1 hour                          | Email                            |
| P4 escalation | 4 hours                         | Email / Portal                   |

If acknowledgement not received:

- Retry per defined attempts
- Move to backup contact
- Trigger emergency override if necessary

---

# 13. Escalation Logging (Mandatory)

Every escalation must be logged in the incident ticket with:

| Field                                      | Required |
| ------------------------------------------ | -------- |
| Date/time of escalation (UTC)              | Yes      |
| Escalation level (L1, L2, L3, etc.)        | Yes      |
| Contact attempted                          | Yes      |
| Method (phone/email/etc.)                  | Yes      |
| Outcome (acknowledged/unreachable)         | Yes      |
| Time to acknowledgement                    | Yes      |
| Backup contacted (if applicable)           | Yes      |
| Emergency override invoked (if applicable) | Yes      |
| Notes                                      | Yes      |

---

# 14. Quick Reference Card (Mandatory)

> Single-page summary for analysts during P1 incidents.

## 14.1 P1 Immediate Contacts

| Priority | Role                          | Contact      | Phone         |
| -------- | ----------------------------- | ------------ | ------------- |
| 1        | Client 24x7 On-Call (Primary) | `[Name]`     | `[Number]`    |
| 2        | Client 24x7 On-Call (Backup)  | `[Name]`     | `[Number]`    |
| 3        | Client Security Lead          | `[Name]`     | `[Number]`    |
| 4        | Client CISO                   | `[Name]`     | `[Number]`    |
| 5        | MSSP SOC Lead (on-shift)      | Per rotation | Bridge number |
| 6        | MSSP SOC Manager              | `[Name]`     | `[Number]`    |

## 14.2 Special Scenario Quick Contacts

| Scenario                            | Contact                                    |
| ----------------------------------- | ------------------------------------------ |
| Regulatory Reportable (RBI/CERT-In) | Client Compliance Officer + Client CISO    |
| Customer Data Breach                | Client DPO + Legal + CISO + Communications |
| Insider Threat                      | Client HR + Legal + Security               |
| Material Incident → Board           | Client CEO/MD + CISO + Communications      |
| Media Inquiry                       | Client Communications + Legal + CISO       |
| Crisis Bridge                       | Conference Number: `[Bridge URL/Number]`   |
| Cyber Insurance                     | Client Risk Mgmt                           |
| Law Enforcement                     | Client Legal → Designated coordinator      |

---

# 15. Periodic Validation (Mandatory)

| Validation Type                                 | Frequency |
| ----------------------------------------------- | --------- |
| Contact verification (email + phone reach test) | Quarterly |
| 24x7 on-call test call (announced)              | Quarterly |
| Full escalation drill (tabletop)                | Annually  |
| Bridge call drill                               | Quarterly |
| Emergency override simulation                   | Annually  |

---

# 16. Change Management (Mandatory)

Any change to this matrix requires:

| Change Type                   | Approval                                    |
| ----------------------------- | ------------------------------------------- |
| Contact info update           | SDM updates within 48 hours of notification |
| Reach SLA change              | Joint approval (SOC Manager + Client CISO)  |
| Escalation path restructure   | Joint approval (SOC Manager + Client CISO)  |
| New escalation scenario added | Joint approval                              |
| Authority change              | Joint approval (CISO both sides)            |

Changes must be:

- Logged with date, change, rationale, approver
- Communicated to SOC team within 24 hours of approval
- Validated via test communication

---

# 17. Quality Checklist (Per Matrix)

Before approving the matrix:

- [ ] All severity levels (P1-P4) covered
- [ ] Primary + backup contacts at every level
- [ ] Reach SLAs defined for every contact
- [ ] 24x7 coverage explicitly documented
- [ ] After-hours / weekend coverage included
- [ ] Emergency override defined
- [ ] All scenario paths (regulatory, legal, HR, crisis, customer, vendor) included
- [ ] Containment authority escalation aligned with policy
- [ ] Regulatory reporting timelines aligned (RBI 2-6 hr, CERT-In 6 hr)
- [ ] Crisis bridge participants defined
- [ ] SLA breach escalation defined
- [ ] Acknowledgement standards defined
- [ ] Escalation logging requirements defined
- [ ] Quick reference card included
- [ ] Linked to Client IR Policy
- [ ] Linked to Client IR Contacts
- [ ] Periodic validation schedule defined
- [ ] Change management defined
- [ ] Client approved
- [ ] Tenant segregation verified
- [ ] Classification: Client Restricted

---

# 18. MSSP Considerations (Mandatory)

| Aspect             | Requirement                                   |
| ------------------ | --------------------------------------------- |
| Tenant segregation | Strict; no cross-client escalation references |
| Access control     | Per-client RBAC enforced                      |
| Confidentiality    | Client Restricted; no external sharing        |
| Coordination       | All client comms through assigned SDM         |
| Audit logging      | All access and use logged                     |
| Retention          | Per client contract and regulatory            |

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 19. Related Documents

| Document                         | Path                                                                                            |
| -------------------------------- | ----------------------------------------------------------------------------------------------- |
| Client IR Policy                 | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/Client-IR-Policy.md`         |
| Client Custom Playbooks          | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/Client-Custom-Playbooks/`    |
| Client-Specific Playbook Guide   | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/Client-Specific-Playbook-Guide.md`         |
| Client Environment Profile       | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`                |
| Client IR Contacts               | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`                                 |
| Client Data Segregation Policy   | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`               |
| Escalation Matrix Master         | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md`             |
| L1-to-L2 Escalation              | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L1-to-L2-Escalation.md`                  |
| L2-to-L3 Escalation              | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L2-to-L3-Escalation.md`                  |
| L3-to-IR-Team Escalation         | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L3-to-IR-Team-Escalation.md`             |
| IR-Team-to-Management Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/IR-Team-to-Management-Escalation.md`     |
| Internal-to-MSSP Escalation      | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`          |
| Emergency Escalation P1          | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md`              |
| Bridge Call Agenda Template      | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Bridge-Call-Agenda-Template.md`   |
| RBI Mandatory Report Template    | `07_REPORTING/07.4_Regulatory-Reports/RBI-Mandatory-Report-Template.md`                         |
| CERT-In Reporting SOP            | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`        |
| Legal Counsel Engagement SOP     | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| MSSP-Client SLA Template         | `00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`                                    |
| SLA Breach Escalation Procedure  | `00_GOVERNANCE/00.4_SLA-and-SLO/SLA-Breach-Escalation-Procedure.md`                             |

---

# 20. Revision History

| Version | Date           | Author                 | Changes               |
| ------- | -------------- | ---------------------- | --------------------- |
| 1.0     | `[YYYY-MM-DD]` | MSSP SDM / Client CISO | Initial joint version |

---

# 21. Approval

**Approved by (MSSP):**

| Role             | Name | Signature | Date |
| ---------------- | ---- | --------- | ---- |
| MSSP SDM         |      |           |      |
| MSSP SOC Manager |      |           |      |

**Approved by (Client):**

| Role                   | Name | Signature | Date |
| ---------------------- | ---- | --------- | ---- |
| Client Primary Contact |      |           |      |
| Client CISO            |      |           |      |

---

**End of Document**
