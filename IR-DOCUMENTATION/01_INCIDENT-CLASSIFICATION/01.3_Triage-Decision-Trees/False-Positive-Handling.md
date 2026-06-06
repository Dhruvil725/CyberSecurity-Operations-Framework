# False Positive Handling (SOC Standard)

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | False Positive Handling |
| Document ID | IR-TRIAGE-003 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Purpose

This document defines the standard process for identifying, validating,
documenting, and closing false positive alerts in a consistent and
audit-ready manner.

It ensures that:
- analysts do not waste time repeatedly investigating known noise
- false positives are closed with defensible evidence
- detection rules are tuned continuously to reduce alert fatigue
- SLA/SLO metrics remain meaningful and accurate
- recurring false positives are tracked and prioritized for improvement

---

## 3. Scope

Applies to:
- SIEM alerts and correlations
- EDR alerts
- IDS/IPS/WAF alerts
- cloud and SaaS security alerts
- threat intelligence IOC matches
- user-reported events that prove non-malicious

---

## 4. Definitions

| Term | Definition |
|------|------------|
| False Positive (FP) | Alert triggered by benign activity or incorrect detection logic |
| Benign True Positive (BTP) | Alert triggered correctly but activity is authorized/expected |
| False Negative (FN) | Malicious activity not detected or detected too late |
| Rule Tuning | Adjusting detection logic to reduce false positives while maintaining coverage |
| Suppression | Temporarily preventing repeated noisy alerts (time-boxed) |
| Exception | Formal risk acceptance for a detection or control deviation |

---

## 5. False Positive vs Benign True Positive

Correct classification matters for reporting and tuning.

| Outcome | Detection Correct? | Activity Malicious? | Example |
|--------|---------------------|---------------------|---------|
| False Positive | No | No | rule fires on normal application behavior |
| Benign True Positive | Yes | No | rule fires on authorized admin activity |
| Incident | Yes | Yes | malware execution or account compromise |

Rule of thumb:
- If the rule is wrong: False Positive
- If the rule is correct but activity is legitimate: Benign True Positive

---

## 6. Standard FP Handling Workflow

### Step 1: Confirm the Alert Trigger and Evidence
Capture:
- alert name, rule ID, and source
- timestamp and affected asset/user
- raw log snippet or EDR telemetry that caused alert
- correlation logic (if SIEM)

### Step 2: Perform Minimum Validation (Required Checks)
Perform validation using applicable sources:

- identity logs (sign-in patterns, MFA events)
- EDR process tree and hashes (for endpoint alerts)
- network logs (proxy/firewall/DNS)
- asset context (criticality, owner)
- change records or authorized activity registers
- threat intel reputation for IOCs (if IOC-based alert)

Document exactly what was checked.

### Step 3: Determine FP Type (Classification)
Use one of these FP types:

| FP Type | Description | Example |
|--------|-------------|---------|
| Data Quality FP | Bad parsing, missing fields, duplicate events | malformed logs cause rule match |
| Environment FP | Legitimate software resembles malicious behavior | backup agent triggers suspicious command |
| Rule Logic FP | Rule thresholds too low or too broad | scanning rule triggers on routine admin checks |
| IOC FP | IOC is outdated, misattributed, or benign | domain re-registered and now legitimate |
| Context FP | Alert lacks context and appears suspicious | maintenance action triggered detection |

### Step 4: Close the Alert with Proper Documentation
Ticket must include:
- disposition: False Positive
- FP type
- evidence summary
- reason for closure
- recommendation: tune, suppress, whitelist, or accept risk

### Step 5: Create Tuning Task (If Recurring)
If repeated, raise a tuning request with:
- rule name and ID
- FP evidence examples (at least 3 occurrences recommended)
- proposed adjustment
- business justification and risk assessment
- owner and due date

Reference: `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md`

---

## 7. Minimum Documentation Standard (FP Ticket Template)

Paste this into ticket notes when closing as FP:

- Alert Source:
- Rule Name / ID:
- Detection Timestamp:
- Affected Asset(s):
- Affected User(s):
- Validation Performed:
  - Identity logs checked: Yes/No
  - EDR telemetry checked: Yes/No
  - Proxy/Firewall/DNS checked: Yes/No
  - Change/maintenance check: Yes/No
  - Threat intel check: Yes/No
- Evidence Summary:
- FP Classification Type:
- Reason for Closure:
- Recommended Action:
  - tuning required: Yes/No
  - suppression required: Yes/No
  - whitelist required: Yes/No
- Approver (if required):
- Closure Timestamp:

---

## 8. When FP Closure Requires Approval

FP can be closed by L1 for low-risk alerts; approval is required in the
following cases:

| Condition | Approval Required |
|----------|-------------------|
| Alert initially classified as P1 or P2 | SOC Lead approval |
| Alert involves privileged accounts | SOC Lead approval |
| Alert involves critical servers | SOC Lead approval |
| Alert relates to data exfiltration indicators | L2/SOC Lead approval |
| Alert relates to malware execution indicators | L2/SOC Lead approval |
| FP requires whitelist or permanent exclusion | SOC Lead + Tool Owner approval |
| Alert involves regulated client environment (MSSP) | SOC Lead + SDM approval (as required by contract) |

---

## 9. Suppression vs Whitelisting vs Tuning (Decision Guidance)

| Option | When to Use | Risk Consideration |
|--------|-------------|-------------------|
| Tuning | Recurring FP due to broad logic | Best long-term fix; may require testing |
| Suppression | High noise temporarily while tuning work is planned | Must be time-boxed and reviewed |
| Whitelisting | Activity is legitimate and repeated (known safe) | High risk if abused; requires approval |
| Exception | Detection noise accepted due to business constraints | Must be documented in exception register |

Reference:
- `00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md`
- `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Exclusion-Management.md`

---

## 10. False Positive Trend Management

### 10.1 FP Tracking Metrics
Track monthly:
- FP rate overall (FP / total alerts)
- FP rate per rule
- FP rate per log source
- top 10 noisy rules
- tuning backlog size
- time to implement tuning

Reference: `00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`

### 10.2 FP Thresholds (Operational Targets)
Recommended operational thresholds:

| Metric | Target |
|--------|--------|
| Overall FP rate | 30 percent or less |
| Noisy rule threshold | Any single rule producing more than 50 alerts per day |
| Tuning turnaround time | 30 days for high noise, 7 days for critical noise |

Targets may be adjusted based on SOC size and tool maturity.

---

## 11. Common FP Root Causes and Recommended Fixes

| Root Cause | Example | Recommended Fix |
|-----------|---------|-----------------|
| Missing context | alert lacks asset criticality | enrich with CMDB or asset tags |
| Poor parsing | field extraction incorrect | fix parser and normalization |
| Over-broad detection | threshold too low | tighten logic, add exclusions |
| Business workflow changes | new tool rollout triggers alerts | update rule to include new tool signature |
| IOC quality issues | false TI matches | validate feeds, add confidence scoring |
| Legitimate admin scripts | automation triggers detections | whitelist script hash + sign scripts |

---

## 12. MSSP-Specific FP Handling Rules

For MSSP operations:

- do not copy evidence from one client into another client ticket
- ensure tenant segregation and correct client attribution
- apply client-specific allow lists only after client approval
- document client approval for whitelisting decisions
- recurring client-specific FPs should result in client-specific tuning or scoped suppression

Reference: `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/`

---

## 13. Related Documents

| Document | Path |
|---------|------|
| Master Triage Decision Tree | `01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/Master-Triage-Decision-Tree.md` |
| Alert-to-Incident Qualification | `01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/Alert-to-Incident-Qualification.md` |
| SIEM Alert Tuning Guide | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md` |
| EDR Exclusion Management | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Exclusion-Management.md` |
| Policy Exception Register | `00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md` |
| Monthly Metrics Report | `07_REPORTING/07.2_Operational-Reports/Monthly-Metrics-Report.md` |

---

## 14. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | SOC Manager | Initial version |

---

## 15. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

End of Document