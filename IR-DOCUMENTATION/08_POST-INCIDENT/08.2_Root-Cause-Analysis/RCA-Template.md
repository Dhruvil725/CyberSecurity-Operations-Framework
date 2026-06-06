# Root Cause Analysis (RCA) Template

---

# 1. Document Control

| Field          | Value                                |
| -------------- | ------------------------------------ |
| Document Name  | Template – Root Cause Analysis (RCA) |
| Document ID    | RCA-TPL-001                          |
| Version        | 1.0                                  |
| Effective Date | 30-May-2026                          |
| Owner          | IR Team Lead / SOC Manager           |
| Approved By    | CISO                                 |
| Classification | Internal – Confidential              |
| Review Cycle   | Annually                             |

---

# 2. Purpose

This template provides the standardized **Root Cause Analysis (RCA)** format used to systematically identify, document, and address the underlying causes of cyber security incidents.

RCA is critical because:

- treating symptoms without addressing root cause leads to incident recurrence
- NIST SP 800-61 emphasizes root cause identification in post-incident activity
- ISO 27001 Annex A.5.27 requires learning from incidents through structured analysis
- RBI Cyber Security Framework mandates RCA for material incidents (within 14–30 days)
- regulators and auditors expect documented RCA with corrective actions
- MSSP clients require RCA reports as part of incident closure deliverables
- RCA feeds into preventive controls, detection engineering, and process improvements
- repeated incidents indicate uncompleted or ineffective RCA

This template ensures:

- consistent RCA methodology across all incidents
- evidence-based root cause identification
- clear distinction between root cause, contributing factors, and symptoms
- traceable corrective and preventive actions
- audit-ready documentation linked to incident records
- linkage to Lessons Learned, improvement registers, and detection updates

Reference alignment:
`00_GOVERNANCE/00.1_Policies/IR-Policy-Master.md`
`08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`

---

# 3. Scope

This RCA template is used for:

| Scenario                             | RCA Required?                  | Timeline Post-Closure                    |
| ------------------------------------ | ------------------------------ | ---------------------------------------- |
| P1 incidents                         | **Mandatory**                  | Within 10 working days                   |
| P2 incidents                         | **Mandatory**                  | Within 15 working days                   |
| P3 incidents (TP, significant)       | **Recommended**                | Within 20 working days                   |
| P4 incidents                         | Optional (if pattern observed) | As needed                                |
| Recurring incidents                  | **Mandatory**                  | Within 10 working days                   |
| Regulatory-reportable incidents      | **Mandatory**                  | Per regulator timeline (RBI: 14–30 days) |
| MSSP client incidents                | Per client SLA                 | Per SLA                                  |
| Near-miss with high potential impact | **Recommended**                | Within 15 working days                   |

Out of scope:

- false positive closures
- routine operational issues without security impact
- minor alerts handled in BAU triage

References:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

# 4. Definitions

| Term                   | Definition                                                                          |
| ---------------------- | ----------------------------------------------------------------------------------- |
| Root Cause             | The fundamental underlying reason an incident occurred; removal prevents recurrence |
| Contributing Factor    | Condition that enabled or worsened the incident but is not the primary cause        |
| Symptom                | Observable manifestation of the incident (e.g., alert, system failure)              |
| Proximate Cause        | Immediate cause that directly triggered the incident                                |
| Latent Cause           | Underlying organizational/systemic weakness contributing to the incident            |
| Corrective Action (CA) | Action to address identified root cause                                             |
| Preventive Action (PA) | Action to prevent recurrence or similar incidents                                   |
| 5 Whys                 | Iterative questioning technique to drill down to root cause                         |
| Fishbone (Ishikawa)    | Diagram method to identify causes across categories                                 |
| Fault Tree Analysis    | Top-down deductive analysis of failure paths                                        |

---

# 5. Roles and Responsibilities

| Role                     | Responsibilities                                                   |
| ------------------------ | ------------------------------------------------------------------ |
| RCA Owner                | Leads RCA; gathers evidence; documents analysis; presents findings |
| IR Team Lead             | Provides technical analysis; validates root cause                  |
| SOC Lead                 | Provides SOC operational context and detection insights            |
| L3 Analyst               | Conducts deep technical investigation supporting RCA               |
| SOC Manager              | Approves RCA; ensures corrective actions are tracked               |
| CISO                     | Reviews RCA for P1/major incidents; approves strategic remediation |
| Compliance Lead          | Ensures RCA meets regulatory requirements                          |
| IT Operations            | Provides infrastructure/operational context                        |
| Business Stakeholder     | Provides business process context                                  |
| MSSP SDM (if applicable) | Coordinates client-facing RCA delivery                             |
| Action Owners            | Execute corrective and preventive actions                          |

---

# 6. RCA Methodology Selection (Mandatory)

Choose appropriate methodology based on incident complexity:

| Methodology             | Best For                                      | Complexity | Reference                 |
| ----------------------- | --------------------------------------------- | ---------- | ------------------------- |
| **5 Whys**              | Simple to moderate incidents; quick analysis  | Low–Medium | `RCA-5-Why-Template.md`   |
| **Fishbone (Ishikawa)** | Multiple potential causes across categories   | Medium     | This template Section 9   |
| **Fault Tree Analysis** | Complex incidents with multiple failure paths | High       | This template Section 10  |
| **Timeline Analysis**   | Incidents with clear sequence of events       | Medium     | `RCA-Timeline-Builder.md` |
| **Combined Approach**   | Major incidents (P1/P2)                       | High       | This template (full)      |

**Recommendation:**

- P1 incidents: Use combined approach (5 Whys + Fishbone + Timeline)
- P2 incidents: Use Fishbone + 5 Whys
- P3 incidents: Use 5 Whys or Timeline
- Recurring incidents: Use Fault Tree Analysis

---

# 7. RCA Principles (Mandatory)

| Principle      | Description                                                          |
| -------------- | -------------------------------------------------------------------- |
| Evidence-based | Every conclusion supported by evidence (logs, timestamps, artifacts) |
| Blameless      | Focus on systems and processes, not individuals                      |
| Systematic     | Follow chosen methodology rigorously                                 |
| Comprehensive  | Consider people, process, technology, and external factors           |
| Honest         | Document what is known, suspected, and unknown                       |
| Traceable      | Every finding linked to evidence reference                           |
| Actionable     | Root cause must enable corrective action                             |
| Validated      | Root cause hypothesis tested against evidence                        |

---

# 8. RCA Template (Copy/Paste)

## 8.1 RCA Metadata (Mandatory)

| Field                         | Value                                         |
| ----------------------------- | --------------------------------------------- |
| RCA ID                        | `RCA-YYYY-####`                               |
| Incident ID / Ticket ID       | `INC-YYYY-####`                               |
| Incident Category             | `...`                                         |
| Incident Severity (Final)     | P1 / P2 / P3 / P4                             |
| Incident Detection Date (UTC) | `YYYY-MM-DD HH:MM`                            |
| Incident Closure Date (UTC)   | `YYYY-MM-DD HH:MM`                            |
| RCA Initiation Date (UTC)     | `YYYY-MM-DD HH:MM`                            |
| RCA Completion Date (UTC)     | `YYYY-MM-DD HH:MM`                            |
| RCA Owner                     | `Name / Role`                                 |
| Contributors                  | `Name, Name, Name`                            |
| Reviewed By                   | `Name / Role`                                 |
| Approved By                   | `Name / Role`                                 |
| Methodology Used              | 5 Whys / Fishbone / FTA / Timeline / Combined |
| Client/Tenant (MSSP only)     | `Client ID / Name`                            |
| Classification                | Internal – Confidential                       |

---

## 8.2 Incident Summary (Mandatory)

- **Brief Description:** `1–2 line summary of incident`
- **Attack Vector:** `Email / Web / Network / Insider / Supply Chain / Other`
- **Affected Systems:** `Count and types`
- **Affected Users:** `Count and categories`
- **Business Impact:** `Service disruption / Data loss / Financial / Reputation`
- **Detection Source:** `SIEM / EDR / User / Threat Intel / Other`
- **Detection Delay (from occurrence):** `Time delta`
- **Containment Duration:** `Time taken`
- **Total Incident Duration:** `Time taken`

---

## 8.3 Problem Statement (Mandatory)

Clearly articulate what went wrong in **one paragraph**:

> *Example: "On [date], an attacker successfully exfiltrated [data type] from [system] over a period of [duration] before detection. The attack exploited [vulnerability/weakness] and was not detected by existing controls until [trigger event]. The incident impacted [scope] and resulted in [business impact]."*

**Your Problem Statement:**

`[Write 3–5 sentence problem statement here]`

---

## 8.4 Evidence Inventory (Mandatory)

| Evidence Type           | Reference ID / Path | Source | Used For                    |
| ----------------------- | ------------------- | ------ | --------------------------- |
| SIEM Logs               |                     |        | Timeline reconstruction     |
| EDR Telemetry           |                     |        | Endpoint behavior analysis  |
| Network Logs / PCAP     |                     |        | Network activity analysis   |
| Firewall Logs           |                     |        | Perimeter activity          |
| Application Logs        |                     |        | Application behavior        |
| Authentication Logs     |                     |        | Access analysis             |
| Email Logs              |                     |        | Email-based attack analysis |
| Disk/Memory Images      |                     |        | Forensic analysis           |
| Configuration Snapshots |                     |        | Control state validation    |
| Change Records          |                     |        | Recent changes review       |
| Threat Intel Reports    |                     |        | TTP correlation             |
| Vendor Advisories       |                     |        | Vulnerability validation    |

References:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/`
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/`

---

## 8.5 Incident Timeline (Mandatory)

| #   | Event                               | Timestamp (UTC) | Source | Evidence Ref |
| --- | ----------------------------------- | --------------- | ------ | ------------ |
| 1   | Initial compromise (estimated)      |                 |        |              |
| 2   | First malicious activity observed   |                 |        |              |
| 3   | Lateral movement (if any)           |                 |        |              |
| 4   | Persistence established             |                 |        |              |
| 5   | Data access / exfiltration (if any) |                 |        |              |
| 6   | First detection                     |                 |        |              |
| 7   | Alert triggered                     |                 |        |              |
| 8   | Triage initiated                    |                 |        |              |
| 9   | Incident declared                   |                 |        |              |
| 10  | Containment initiated               |                 |        |              |
| 11  | Containment achieved                |                 |        |              |
| 12  | Eradication completed               |                 |        |              |
| 13  | Recovery completed                  |                 |        |              |
| 14  | Incident closed                     |                 |        |              |

Reference:
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Timeline-Builder.md`

---

## 8.6 What Happened (Sequence of Events – Mandatory)

Provide a detailed narrative of the incident sequence:

**Phase 1 – Initial Access:**
`Describe how the attacker gained initial access. Reference evidence.`

**Phase 2 – Execution / Establishment:**
`Describe what the attacker did after gaining access. Reference evidence.`

**Phase 3 – Persistence / Privilege Escalation (if applicable):**
`Describe persistence mechanisms and privilege escalation. Reference evidence.`

**Phase 4 – Lateral Movement (if applicable):**
`Describe lateral movement activities. Reference evidence.`

**Phase 5 – Objective (Data Exfiltration / Encryption / Disruption):**
`Describe the attacker's objective and execution. Reference evidence.`

**Phase 6 – Detection:**
`Describe how and when the incident was detected. Reference evidence.`

**Phase 7 – Response:**
`Describe the response actions taken. Reference evidence.`

---

## 8.7 5 Whys Analysis (Mandatory for All RCAs)

Drill down from the visible problem to the root cause:

| Level          | Question               | Answer | Evidence Ref |
| -------------- | ---------------------- | ------ | ------------ |
| **Problem**    | What happened?         |        |              |
| **Why #1**     | Why did this happen?   |        |              |
| **Why #2**     | Why did *that* happen? |        |              |
| **Why #3**     | Why did *that* happen? |        |              |
| **Why #4**     | Why did *that* happen? |        |              |
| **Why #5**     | Why did *that* happen? |        |              |
| **Root Cause** | Identified root cause  |        |              |

**Note:** Stop at 5 Whys unless deeper analysis is needed. If root cause is unclear at level 5, continue.

Reference:
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-5-Why-Template.md`

---

## 8.8 Fishbone (Ishikawa) Analysis (Recommended for P1/P2)

Identify potential causes across categories:

### 8.8.1 People

- `Skills gap?`
- `Awareness gap?`
- `Staffing levels?`
- `Communication breakdown?`

### 8.8.2 Process

- `Missing procedure?`
- `Outdated playbook?`
- `Unclear escalation path?`
- `Inadequate change management?`

### 8.8.3 Technology

- `Tool misconfiguration?`
- `Missing detection rule?`
- `Patching gap?`
- `Architecture weakness?`

### 8.8.4 Environment / External

- `Vendor/supply chain weakness?`
- `Threat landscape change?`
- `Third-party dependency?`
- `Regulatory/compliance gap?`

### 8.8.5 Measurement / Monitoring

- `Detection coverage gap?`
- `Logging gap?`
- `Alert tuning issue?`
- `KPI/metric blind spot?`

### 8.8.6 Materials / Data

- `Outdated threat intel?`
- `Incomplete asset inventory?`
- `Data classification gap?`
- `IOC sharing gap?`

---

## 8.9 Fault Tree Analysis (For Complex Incidents – Optional)

Document failure paths leading to the incident:

```
[TOP EVENT: Incident occurred]
    |
    +-- [Condition 1: Vulnerability existed]
    |       |
    |       +-- Patch not applied
    |       +-- Patch not available
    |
    +-- [Condition 2: Attacker accessed system]
    |       |
    |       +-- Weak authentication
    |       +-- Credentials compromised
    |
    +-- [Condition 3: Detection failed]
            |
            +-- Rule not configured
            +-- Log source missing
            +-- Alert tuned out
```

`[Build your fault tree here based on incident specifics]`

---

## 8.10 Root Cause Identification (Mandatory)

### 8.10.1 Primary Root Cause

**Root Cause Statement:**

`Single, clear statement of the fundamental root cause`

**Evidence Supporting Root Cause:**

- `Evidence reference 1`
- `Evidence reference 2`
- `Evidence reference 3`

**Validation:**

- How was this root cause validated? `...`
- Are alternative explanations ruled out? `Yes / No – with rationale`

### 8.10.2 Contributing Factors

| #   | Contributing Factor | Category                                 | Evidence Ref |
| --- | ------------------- | ---------------------------------------- | ------------ |
| 1   |                     | People / Process / Technology / External |              |
| 2   |                     |                                          |              |
| 3   |                     |                                          |              |

### 8.10.3 Latent / Systemic Issues

| #   | Latent Issue | Description | Implication |
| --- | ------------ | ----------- | ----------- |
| 1   |              |             |             |
| 2   |              |             |             |

---

## 8.11 Why Was It Not Detected Sooner? (Mandatory)

Critical question for every RCA:

| Aspect                          | Analysis | Gap Identified |
| ------------------------------- | -------- | -------------- |
| Was there a detection rule?     | Yes / No |                |
| Was the rule triggered?         | Yes / No |                |
| Was the alert visible to SOC?   | Yes / No |                |
| Was the alert acted upon?       | Yes / No |                |
| Was logging coverage adequate?  | Yes / No |                |
| Was telemetry available?        | Yes / No |                |
| Was threat intel available?     | Yes / No |                |
| Was the attack technique known? | Yes / No |                |

---

## 8.12 Why Did Existing Controls Fail? (Mandatory)

| Control             | Was It In Place? | Did It Function? | Why Did It Fail? |
| ------------------- | ---------------- | ---------------- | ---------------- |
| Preventive controls |                  |                  |                  |
| Detective controls  |                  |                  |                  |
| Responsive controls |                  |                  |                  |
| Recovery controls   |                  |                  |                  |

---

## 8.13 Impact Assessment (Mandatory)

| Impact Category     | Details                                        | Quantification       |
| ------------------- | ---------------------------------------------- | -------------------- |
| Operational Impact  | Service disruption, downtime                   | `Duration / Scope`   |
| Financial Impact    | Direct loss, recovery cost, regulatory penalty | `₹... / USD...`      |
| Data Impact         | Records affected, data classification          | `Count / Categories` |
| Customer Impact     | Customers affected, complaints                 | `Count / Severity`   |
| Reputational Impact | Media coverage, customer trust                 | `Qualitative`        |
| Regulatory Impact   | Reporting obligations, penalties               | `Yes / No`           |
| Legal Impact        | Litigation risk, contractual breach            | `Yes / No`           |

---

## 8.14 Corrective and Preventive Actions (Mandatory)

### 8.14.1 Corrective Actions (Address Root Cause)

| Action ID | Action | Category                            | Owner | Due Date (UTC) | Priority         | Tracking Ref |
| --------- | ------ | ----------------------------------- | ----- | -------------- | ---------------- | ------------ |
| CA-001    |        | People / Process / Tech / Detection |       |                | High / Med / Low |              |
| CA-002    |        |                                     |       |                |                  |              |

### 8.14.2 Preventive Actions (Prevent Recurrence)

| Action ID | Action | Category | Owner | Due Date (UTC) | Priority | Tracking Ref |
| --------- | ------ | -------- | ----- | -------------- | -------- | ------------ |
| PA-001    |        |          |       |                |          |              |
| PA-002    |        |          |       |                |          |              |

### 8.14.3 Detection Improvements

| Action ID | Detection Gap | Improvement | Tool               | Owner | Due Date |
| --------- | ------------- | ----------- | ------------------ | ----- | -------- |
| DI-001    |               |             | SIEM / EDR / Other |       |          |

References:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx`
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`
`08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`

---

## 8.15 Risk Assessment Update (If Applicable)

- **New risks identified?** Yes / No
- **Existing risks materialized?** Yes / No
- **Risk register update required?** Yes / No

| Risk Description | Likelihood       | Impact           | Treatment Plan | Owner |
| ---------------- | ---------------- | ---------------- | -------------- | ----- |
|                  | High / Med / Low | High / Med / Low |                |       |

---

## 8.16 Lessons Learned Summary (Mandatory)

- **Key Insight #1:** `...`
- **Key Insight #2:** `...`
- **Key Insight #3:** `...`

Full LL captured in:
`08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`

---

## 8.17 Unknowns and Limitations (Mandatory)

Document what could not be determined and why:

| Unknown | Reason                                            | Impact on RCA |
| ------- | ------------------------------------------------- | ------------- |
|         | Evidence unavailable / Tool gap / Time constraint |               |

---

## 8.18 Recommendations to Management (P1/P2 Mandatory)

| #   | Recommendation | Rationale | Resource Required | Priority         |
| --- | -------------- | --------- | ----------------- | ---------------- |
| 1   |                |           |                   | High / Med / Low |
| 2   |                |           |                   |                  |

---

# 9. RCA Quality Criteria (Mandatory)

A complete RCA must meet:

| Criterion                              | Met (Y/N) |
| -------------------------------------- | --------- |
| Problem statement clearly articulated  |           |
| Evidence inventory complete            |           |
| Timeline reconstructed with evidence   |           |
| 5 Whys analysis performed              |           |
| Root cause supported by evidence       |           |
| Alternative explanations considered    |           |
| Contributing factors identified        |           |
| Detection gap analyzed                 |           |
| Control failures analyzed              |           |
| Impact quantified                      |           |
| Corrective actions defined with owners |           |
| Preventive actions defined with owners |           |
| Unknowns documented                    |           |
| Approval obtained                      |           |

---

# 10. RCA Review and Approval Process

## 10.1 Internal Review

1. RCA Owner drafts RCA within timeline
2. IR Team Lead reviews technical accuracy
3. SOC Manager reviews completeness
4. Compliance Lead reviews regulatory alignment
5. CISO approves (P1/P2)

## 10.2 Distribution

| Audience                     | Version Shared                  |
| ---------------------------- | ------------------------------- |
| SOC Team                     | Full internal version           |
| CISO / Executive Management  | Executive summary + key actions |
| Board / Audit Committee (P1) | Executive summary               |
| Compliance / Legal           | Full version                    |
| MSSP Client (if applicable)  | Sanitized client version        |
| Regulators (if mandated)     | Per regulatory format           |

References:
`07_REPORTING/07.1_Incident-Reports/Executive-Summary-Template.md`
`07_REPORTING/07.4_Regulatory-Reports/RBI-Mandatory-Report-Template.md`

---

# 11. MSSP Considerations (If Applicable)

For MSSP-managed clients:

- RCA must be **tenant-scoped**; no cross-client data
- Client-facing version must be **sanitized** of internal MSSP details
- Client review/approval may be required per SLA
- Client-specific corrective actions tracked in client folder
- MSSP-internal RCA maintained for service improvement
- Cross-client trends analyzed only in **aggregated, anonymized form**
- RCA delivery timeline must meet client SLA
- Evidence shared with client must follow CoC if evidence-grade

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`
`07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Incident-Report-Template.md`

---

# 12. Common RCA Pitfalls to Avoid

| Pitfall                                    | Mitigation                               |
| ------------------------------------------ | ---------------------------------------- |
| Stopping at symptoms instead of root cause | Use 5 Whys rigorously                    |
| Blaming individuals                        | Maintain blameless focus on systems      |
| Single root cause assumption               | Consider multiple contributing factors   |
| Lack of evidence                           | Reference evidence for every conclusion  |
| Vague action items                         | Use SMART criteria with owners and dates |
| No follow-up tracking                      | Log actions in improvement register      |
| Skipping detection gap analysis            | Always analyze why detection failed      |
| Not documenting unknowns                   | Be honest about limitations              |
| Rushed RCA                                 | Follow timeline but ensure quality       |
| Ignoring near-misses                       | Analyze near-misses for preventive value |

---

# 13. Related Documents

| Document                       | Path                                                                            |
| ------------------------------ | ------------------------------------------------------------------------------- |
| RCA 5-Why Template             | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-5-Why-Template.md`               |
| RCA Timeline Builder           | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Timeline-Builder.md`             |
| Lessons Learned Template       | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`             |
| PIR Meeting Agenda             | `08_POST-INCIDENT/08.1_Lessons-Learned/PIR-Meeting-Agenda.md`                   |
| Action Items Tracker           | `08_POST-INCIDENT/08.1_Lessons-Learned/Action-Items-Tracker.xlsx`               |
| Security Improvement Register  | `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx` |
| Detection Improvement Log      | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`       |
| Playbook Update Log            | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`             |
| Final Incident Report Template | `07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md`          |
| RBI Mandatory Report Template  | `07_REPORTING/07.4_Regulatory-Reports/RBI-Mandatory-Report-Template.md`         |
| L3 Root Cause Analysis SOP     | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Root-Cause-Analysis.md`           |

---

# 14. Revision History

| Version | Date        | Author                     | Changes         |
| ------- | ----------- | -------------------------- | --------------- |
| 1.0     | 30-May-2026 | IR Team Lead / SOC Manager | Initial version |

---

# 15. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**
